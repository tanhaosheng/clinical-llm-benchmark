# Contributing — submit your own model run

This benchmark is designed to grow through replication. If you evaluate a model with the
framework, your result can be added to the comparison.

## How to submit

1. **Fork** this repo and create a branch, or open an issue with your scorecard.
2. Run the prompt in [`case-template.md`](case-template.md) **3 times** on your model (free tier is fine).
3. Score each run item-by-item with the rubric in [`framework.md`](framework.md) (§2 + the answer key in §3).
4. Report, per run, at minimum:
   - model name + interface + tier + input modality (text/image)
   - the 3 total scores / 100
   - max−min (stability; ≥ 8 ⇒ unstable)
   - guideline-section citation accuracy (n / 16)
   - output language
5. Open a **Pull Request** adding a row to `results/` (new file `results/<model>.md` preferred), or paste the scorecard in an issue.

## Rules

- Keep the **prompt identical** to `case-template.md`; if you must change it, say so explicitly and treat the run as a separate track.
- Note any **input-modality asymmetry** (text vs image) — it is a stated limitation, not a defect of your submission.
- De-identified cases only. **No real patient identifiers.**
- This is a research/education benchmark. **Model output is not clinical advice.**

## What gets merged

Runs that follow the rubric and disclose model/tier/modality will be merged. We especially welcome:
- additional Chinese free-tier / paid models (Qwen, GLM, Kimi, Hunyuan, …);
- the same case on **image input** vs **text input** for the same model (controlled comparison);
- extension to a **second case** (different stage / subtype) to test generalizability.
