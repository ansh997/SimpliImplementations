```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM
import numpy as np

# Load models
draft_model_name = "gpt2"  # smaller/faster model
target_model_name = "gpt2-large"  # bigger/slower model

tokenizer = AutoTokenizer.from_pretrained(draft_model_name)
draft_model = AutoModelForCausalLM.from_pretrained(draft_model_name).cuda().eval()
target_model = AutoModelForCausalLM.from_pretrained(target_model_name).cuda().eval()

# Sampling parameters
num_draft_tokens = 5
max_length = 50

# Prompt
prompt = "Once upon a time"
input_ids = tokenizer(prompt, return_tensors="pt").input_ids.cuda()

# Main loop
generated = input_ids.clone()

while generated.shape[1] < max_length:

    # Step 1: Draft model proposes k tokens
    with torch.no_grad():
        draft_output = draft_model.generate(
            generated,
            max_new_tokens=num_draft_tokens,
            do_sample=True,
            temperature=1.0,
            top_k=50
        )
    
    proposed_tokens = draft_output[:, generated.shape[1]:]  # shape: [1, num_draft_tokens]

    # Step 2: Target model verifies draft tokens
    # Feed full sequence (prompt + proposed tokens) to target model
    full_sequence = torch.cat([generated, proposed_tokens], dim=1)
    
    with torch.no_grad():
        target_logits = target_model(full_sequence).logits

    # For each proposed token, calculate acceptance probability
    accept_until = 0

    for i in range(num_draft_tokens):
        token_pos = generated.shape[1] + i  # position of proposed token

        # Target model probability for proposed token
        target_logit = target_logits[:, token_pos - 1, :]  # logit predicting proposed_tokens[:, i]
        target_probs = torch.softmax(target_logit, dim=-1)
        target_prob = target_probs[:, proposed_tokens[:, i]].item()

        # Draft model probability for proposed token (recompute for this token)
        with torch.no_grad():
            draft_logits = draft_model(full_sequence[:, :token_pos]).logits[:, -1, :]
            draft_probs = torch.softmax(draft_logits, dim=-1)
            draft_prob = draft_probs[:, proposed_tokens[:, i]].item()

        # Acceptance probability
        a = min(1.0, target_prob / (draft_prob + 1e-9))  # small epsilon for stability

        # Sample acceptance
        if np.random.rand() <= a:
            accept_until += 1
        else:
            break  # stop verifying further tokens after first rejection

    # Step 3: Commit accepted tokens
    if accept_until > 0:
        accepted_tokens = proposed_tokens[:, :accept_until]
        generated = torch.cat([generated, accepted_tokens], dim=1)

    # Step 4: If rejected early, generate one token from target model directly
    if accept_until < num_draft_tokens:
        with torch.no_grad():
            target_logits = target_model(generated).logits[:, -1, :]
            target_probs = torch.softmax(target_logits, dim=-1)
            next_token = torch.multinomial(target_probs, num_samples=1)
        generated = torch.cat([generated, next_token], dim=1)

# Decode final output
output_text = tokenizer.decode(generated[0], skip_special_tokens=True)
print(output_text)
```

---

### Helper Functions you would have to fully implement in production:

| Function                                      | Purpose                                            | Input                                                  | Output                   |
| --------------------------------------------- | -------------------------------------------------- | ------------------------------------------------------ | ------------------------ |
| `compute_prob(model, context, target_token)`  | Compute probability of target\_token given context | `model: LM`, `context: Tensor`, `target_token: Tensor` | `prob: float`            |
| `propose_k_tokens(draft_model, input_ids, k)` | Generate k tokens using draft model                | `draft_model: LM`, `input_ids: Tensor`, `k: int`       | `Tensor of shape [1, k]` |

