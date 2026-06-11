# Research Log

## 2026-06-11 — Day 1: Setup
**Did:** Set up stack on Kaggle (Colab free tier didn't work as system RAM died loading
gemma-2-2b; tried fixing with bfloat16 + from_pretrained_no_processing, then moved to
Kaggle T4). Loaded gemma-2-2b + Gemma Scope SAE (layer 12, 16k, canonical).
Ran first feature readout.

**Saw:** 87/16384 features active on last token of a pushy conspiracy prompt about the Moon Landing being fake
-Top feature 7283 = "a interrogative punctuation marks or questions" per Neuronpedia.
Syntax feature fires because the prompt ends in a question. Not sycophancy-relevant.

-Feature 2620 = "words associated with authority, control, and criticism of governance"
Authoritative language is what sycophantic models defer to. Possibly sycophancy-relevant. 

-Feature 2291 = "structural and formatting markers of academic/technical documents, especially LaTeX/Markdown elements and section-style headings."
No LaTex markers or technical documents in input. Not syncophancy-relevant. 


**What I learned today:**
- An SAE takes in an activation vector at one specific point and returns for each feature how strongly that feature was activated
- A feature is one entry in the SAE's dictionary: a direction in activation space corresponding to a concept like "questions" or "authoritative tone"
    - A feature's activiation determines how present that feature is in the input
- A hook is a function attached to a point in the model's forward pass. When computation reaches that point, the model calls the function and hands it the live activation and it completes an action with it
-LLM's break text into tokens, which become vectors. Each vector goes through layers where some element gets computed(Either attention or MLP which gets computed with matrix multiplication with weights) and added back on. The final token gets a "score" for every word in the vocabulary. 
**Next:** Spy/vandal hook. Then Day 2: build ~30 contrastive prompt pairs
(opinionated vs neutral), diff feature activations, and rank candidates.
