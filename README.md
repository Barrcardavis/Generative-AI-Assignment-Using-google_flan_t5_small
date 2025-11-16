# Generative AI with Pre‑trained LLMs  
**Author:** David Davis  

## Project Overview
This assignment explores how decoding parameters influence the behavior of a pre‑trained Large Language Model (Flan‑T5 Small).  
The chosen task is **translation**, using the prompt:

> Translate English to French: *"The weather is nice today."*

Two parameter sweeps were conducted: **temperature** and **top‑p sampling**.  
The goal was to analyze how these parameters affect translation fidelity, coherence, and creativity.
https://youtu.be/uoR2NBsQrVY

---

## Environment Setup
- Framework: Hugging Face Transformers  
- Backend: PyTorch  
- Packages installed:
  ```bash
  pip install transformers torch

  ### Results Comparison: Temperature Sweep
| Test Case | Parameter Setting | Output | Notes |
|-----------|------------------|--------|-------|
| 1 | Greedy (default) | La météo est très agréable aujourd'hui. | Accurate French translation; deterministic and fluent. |
| 2 | temperature=0.7 | L'atmosphère est très nice today. | Mixed French/English; creativity increased, coherence decreased. |
| 3 | temperature=1.0 | The weather is nice today. | Reverted to English; high randomness undermined fidelity. |

**Observation:**  
- Lower temperature produced the most reliable translation.  
- Increasing temperature introduced creativity but reduced accuracy.  
- At high temperature, the model abandoned translation entirely.  
This demonstrates the trade‑off between **determinism vs. diversity**.

### Results Comparison: Top‑p Sweep
| Test Case | Parameter Setting | Output | Notes |
|-----------|------------------|--------|-------|
| 4 | top_p=0.7 | La météo est agréable aujourd'hui. | Faithful translation; conservative sampling close to baseline. |
| 5 | top_p=0.9 | La température serait légèrement proche. | Meaning drift; variation introduced at the expense of accuracy. |
| 6 | top_p=1.0 | Le temps est très bien. | Fluent but simplified; freer rewording reduced precision. |

**Observation:**  
- Conservative top‑p yielded the most accurate translation.  
- Moderate top‑p introduced creative variation but reduced precision.  
- Very open top‑p produced natural phrasing but less faithful translation.  
This demonstrates the trade‑off between **sampling diversity vs. translation fidelity**.
