# Simplimentations

**Simplimentations — Simple Implementations of Complex Ideas**

---

> *"The best way to understand something is to build a small, working version of it."*

---

## Overview

**Simplimentations** is a collection of minimal, readable implementations of complex AI/ML concepts. The goal is to make cutting-edge ideas **approachable** without sacrificing correctness.

This repository serves both as:

* An educational resource for **beginners** who want to see theory translated into code.
* A reference for **researchers** who want clean, minimal baselines to test and experiment with.

---

## Why Simplimentations?

Modern ML research often comes with:

* Long papers with dense math.
* Codebases that are highly abstracted or production-optimized.
* Complex pipelines that hide the core idea.

This repo tries to **strip away unnecessary complexity** and offer:

✅ Minimal code

✅ Clear mappings from theory to implementation

✅ Focus on *core logic*, not engineering boilerplate

---

## Repository Structure

Each concept has:

* A **single Python file** implementing the core idea.
* In-code comments explaining each step.
* References to original papers.

---

## Implementations

| Concept                  | File                                                   | Notes                                                                                      |
| ------------------------ | ------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| **Speculative Decoding** | [`speculative_decoding.py`](./speculative_decoding.py) | Minimal PyTorch implementation of speculative sampling for large language model inference. |
| *(more to be added)*     |                                                        |                                                                                            |

---

## Quick Start

1️⃣ Clone the repository:

```bash
git clone https://github.com/your-username/simplimentations.git
cd simplimentations
```

2️⃣ Install dependencies:

```bash
pip install -r requirements.txt
```

3️⃣ Run any implementation:

```bash
python speculative_decoding.py
```

---

## Dependencies

* `torch`
* `transformers`
* `numpy`

(*Kept minimal for easy reproducibility.*)

---

## Citations & References

The implementations are simplified versions based on the following original research:

* **Speculative Decoding:**
  Chen et al., *"Accelerating Large Language Model Decoding with Speculative Sampling"*
  [arXiv:2302.01318](https://arxiv.org/abs/2302.01318)

Each script cites specific papers and algorithms it's based on.

---

## Who is this repo for?

* 🤖 **Students / Beginners**
  See how papers translate directly into code.

* 🔬 **Researchers / Practitioners**
  Use these as minimal baselines or for rapid prototyping.

* 💡 **Educators / Mentors**
  Use these examples as teaching material.

---

## Contributions

**PRs are welcome!**

If you have:

* A complex concept you've simplified
* A minimal implementation following the repo philosophy
* Clean code with in-code citations

…feel free to open a pull request.

---

## License

MIT License.

---

## Notes

**Simplimentations** is intentionally **not optimized for production**.
The focus is on *clarity* > *performance*.
