# Contributing to Simplimentations

Thank you for your interest in contributing!

**Simplimentations** aims to build minimal, clear, and educational implementations of complex AI/ML concepts. We welcome contributions that align with this goal.

---

## Philosophy

* ✅ Minimal and complete
* ✅ Focused on **clarity of core ideas**
* ✅ Few abstractions; avoid unnecessary classes, frameworks, or over-engineering
* ✅ Clean, readable code with comments
* ✅ Cite original papers in the code

---

## Contribution Guidelines

### 1️⃣ Choose a Concept

* Pick a paper or algorithm that fits the repo's scope:

  * ML fundamentals
  * Recent research (especially LLMs, optimization, inference, etc.)
  * Popular but often abstracted algorithms

### 2️⃣ Keep It Simple

* **One file per concept** (unless there's a very strong reason to modularize)
* Focus on the **core algorithm**, not engineering infrastructure
* Avoid unnecessary external libraries
* Use standard Python, PyTorch, NumPy, or well-known open libraries (e.g., `transformers`)

### 3️⃣ Code Style

* Use consistent formatting (PEP8 / black)
* Comment key steps in the code to explain reasoning
* Write code that a **beginner can read and understand**

### 4️⃣ In-Code Citations

At the top of your file, include:

```python
"""
Title: Name of the Paper
Authors: Author names
Link: https://arxiv.org/abs/XXXX.XXXXX
Original Idea Summary: A 2-3 line plain English summary
"""
```

Example:

```python
"""
Title: Accelerating Large Language Model Decoding with Speculative Sampling
Authors: Chen et al.
Link: https://arxiv.org/abs/2302.01318
Original Idea Summary: Use a small draft model to propose tokens, then verify with the target model.
"""
```

### 5️⃣ Testing

* The script should run standalone.
* Provide a simple example run.
* Avoid large downloads or massive models unless necessary.

### 6️⃣ Pull Request

When opening a pull request:

* Describe what concept you're adding
* Mention the paper(s) you're implementing
* Confirm that your code follows the repo's philosophy

---

## What We Don't Want

🚫 Large, highly abstracted libraries

🚫 Full production pipelines

🚫 Over-engineered code

🚫 Complex configuration management

---

## Questions?

* Feel free to open an issue if you want feedback on an idea before implementing it.
* Or if you're unsure whether a concept fits, just ask!

---

<p align="center"><strong><em>Let's make complex ideas simple, together.</em></strong></p>

---
