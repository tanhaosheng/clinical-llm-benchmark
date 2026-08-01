# Clinical LLM Benchmark — Breast-Cancer Adjuvant-Decision Reasoning vs the 2026 CBCS Guideline

> A reproducible, clinician-authored framework for scoring free-tier Chinese LLMs on guideline-concordant oncology reasoning. Released openly so others can replicate or extend it.

This repository contains the **full evaluation framework** behind the benchmark published at **[tanhaosheng.asia/clinical-benchmark](https://tanhaosheng.asia/clinical-benchmark/)** — a single de-identified post-operative breast-cancer case scored item-by-item (a 16-item / 100-point rubric) against the *2026 Chinese Breast Cancer Society (CBCS) Guideline*.

## What's inside

| File | Description |
|------|-------------|
| `framework.md` | The complete methodology: case design, the 16-item / 100-point scoring rubric, answer key, stability protocol, and disclaimers (Chinese, as used in the live evaluation). |
| `case-template.md` | The exact, copy-pasteable standardized prompt (bilingual: Chinese original + English verbatim) used to query each model. |
| `preprint/clinical_benchmark_preprint.md` | A complete, submission-ready preprint manuscript (medRxiv / arXiv format) describing the method and results. |
| `results/deepseek-vs-chatglm.md` | Headline results: item-level scorecards and stability for DeepSeek Fast vs ChatGLM 5.2. |
| `CONTRIBUTING.md` | How to submit your own model run so it can be added to the comparison. |

## Why this exists

Free-tier LLMs are increasingly used by clinicians for decision support, yet their reliability on **guideline-concordant** oncology reasoning is poorly quantified — especially for Chinese-language guidelines. This benchmark:

- uses a **real, de-identified** case (not a synthetic quiz);
- scores models on a **transparent, weighted rubric** where citing the guideline is required to earn full marks;
- flags **stability** (run-to-run variance) as a first-class metric;
- is **zero-cost and reproducible** (free-tier models, no API spend).

## Headline results (DeepSeek Fast vs ChatGLM 5.2, free tier)

| Metric | DeepSeek Fast | ChatGLM 5.2 |
|---|---|---|
| Median score / 100 | **28** | **5** |
| Stability (max−min) | 0 (perfect) | 8 (unstable) |
| Guideline-section citations | 0 / 16 | 0 / 16 |
| Output language | Chinese | English (all runs) |

**Both models failed the three highest-weight clinical items** and achieved 0/16 citation accuracy — neither is safe for standalone clinical use. See `results/deepseek-vs-chatglm.md` and the preprint for details.

## Reproduce it

1. Copy `case-template.md` and paste it into any model you want to test.
2. Apply `framework.md`'s rubric (§2 and the answer key in §3) item-by-item to the model's full answer.
3. Run **3 times**; flag as unstable if max−min ≥ 8.
4. Submit your scorecard via `CONTRIBUTING.md`.

## Citation

If you use this framework, please cite:

> Tan H. A clinician-authored benchmark of free-tier Chinese LLMs on breast-cancer adjuvant-decision reasoning against the 2026 CBCS guideline. 2026. https://tanhaosheng.asia/clinical-benchmark/

## License

- Code, prompt, and rubric: **MIT** (see `LICENSE`).
- The preprint text: **CC-BY-4.0**.
- The benchmark is for research and education only and **does not constitute clinical advice**.

---

*Authored by Tan Haosheng, MD, PhD — Department of Thyroid and Breast Surgery, Taizhou People's Hospital. Maintained alongside [tanhaosheng.asia](https://tanhaosheng.asia/), a site on AI tools for surgeons.*
