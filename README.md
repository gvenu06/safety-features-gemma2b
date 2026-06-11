# Sycophancy Features in Gemma 2 2B

Independent mechanistic interpretability project: finding and causally testing
sparse autoencoder (SAE) features linked to sycophancy in Gemma 2 2B.

**Status: in progress** (started June 2026). See [research_log.md](research_log.md)
for day-by-day progress

## Research question
Can SAE features in Gemma 2 2B's residual stream identify — and causally
mediate — sycophantic behavior (the model agreeing with a user's stated
opinion instead of answering honestly)? And does steering those features
work better than just prompting the model to be honest?

## Approach

1. **Find** — contrastive activation analysis: run paired prompts (opinionated
   vs. neutral phrasings of the same question) and rank features by
   differential activation.
2. **Verify** — feature ablation and steering via forward hooks, with
   random-feature ablations as controls, to test which candidates actually
   cause the behavior.
3. **Compare** — feature-level steering vs. a prompt-based honesty baseline
   on a held-out sycophancy eval.

## Stack
- Model: `gemma-2-2b` + pre-trained [Gemma Scope](https://huggingface.co/google/gemma-scope)
  SAEs (layer 12 residual stream, 16k width)
- [SAELens](https://github.com/decoderesearch/SAELens) + [TransformerLens](https://github.com/TransformerLensOrg/TransformerLens)
- Runs on a single T4 (Kaggle/Colab)

## Repo

- `notebooks/01_setup_and_explore.ipynb` — load model + SAE, first feature readouts
- `research_log.md` — running log of sessions, results, and mistakes
