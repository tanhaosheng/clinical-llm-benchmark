# Results — DeepSeek Fast vs ChatGLM 5.2 (free tier, 2026 CBCS)

Both models were evaluated on the case in `case-template.md`, scored with the 16-item / 100-point rubric in `framework.md`. Each model was run **3 times** with an identical prompt and unchanged context.

## Overall performance

| Metric | DeepSeek Fast | ChatGLM 5.2 |
|---|---|---|
| Run 1 / 100 | 28 | 10 |
| Run 2 / 100 | 28 | 2 |
| Run 3 / 100 | 28 | 5 |
| Median | **28** | **5** |
| Max−Min (stability) | 0 (perfect) | 8 (unstable) |
| Avg response | ~3–4 s | ~5–8 s |
| Guideline-section citation accuracy | 0 / 16 | 0 / 16 |
| Output language | Chinese | English (all 3 runs) |

## Item-level scorecard (median points)

| # | Item (max) | DeepSeek | ChatGLM |
|---|---|---|---|
| 1.1 | Accept TisN0M0 (6) | 0 | 0 |
| 1.2 | Stage correction (10) | 0 | 0 |
| 1.3 | Molecular subtype (4) | 2 | 2 |
| 2.1 | Surgery + ALND (8) | 4 | 0 |
| 2.2 | Adjuvant RT (4) | 2 | 0 |
| 3.1 | Chemo + multigene (10) | 5 | 0 |
| 3.2a | Endocrine + mastectomy/BCS **(12)** | 0 | 0 |
| 3.2b | AI vs TAM + age **(10)** | 0 | 3 |
| 3.2c | Dose & duration (6) | 3 | 0 |
| 3.2d | OFS/extension/CDK4-6 (6) | 3 | 0 |
| 3.3 | Anti-HER2 (4) | 2 | 0 |
| 4.1 | AE monitoring (6) | 3 | 0 |
| 4.2 | Bone & lifestyle (4) | 2 | 0 |
| 4.3 | Follow-up (4) | 2 | 0 |
| 4.4 | Contralateral + BRCA (4) | 0 | 0 |
| 5 | Self-assessment (2) | 0 | 0 |
| **Total** | | **28** | **5** |

## Three shared high-weight failures (both models)

1. **Never questions staging (items 1.1 + 1.2, 16 pts).** Pathology reports "3 stromal invasion clusters, largest 0.2 cm = 2 mm." Microinvasion is a single focus ≤ 1 mm; 0.2 cm already exceeds it → at least **pT1a (Stage IA)**. Both copied "TisN0M0 Stage 0" without flagging the ambiguity — a safety-level error.
2. **Post-mastectomy DCIS endocrine not downgraded (item 3.2a, 12 pts).** CBCS P59 note a: for DCIS *after mastectomy*, endocrine drugs belong to *chemoprevention*, recommendation downgraded to "consider/optional." Both applied the "DCIS → endocrine strongly recommended" template without distinguishing mastectomy vs breast-conserving surgery.
3. **60-year AI/TAM cutoff omitted (item 3.2b, 10 pts).** CBCS P59 note b: AI's advantage over tamoxifen is mainly in postmenopausal women **< 60**; at ≥ 60 the two are near-equivalent. The patient is exactly 60. Both gave "AI first choice" without writing the cutoff.

## Model-specific notes

- **DeepSeek Fast** — perfectly reproducible (0 variance), Chinese output, correct chemo-exemption (Run 1 also proactively raised Oncotype DX), noted routine tumor markers not recommended, mentioned AI bone/lipid monitoring. Lost all points on the three core items above.
- **ChatGLM 5.2** — all three answers in English despite a Chinese prompt (near-zero usability for Chinese clinicians); ~130 words/run vs DeepSeek ~450; Run 2 scored 2 (essentially restating the case + "let the doctor decide"). Spread = 8 triggered the instability threshold.

## Conclusion

Neither free-tier model is safe for standalone clinical use. Both lack transparent guideline grounding (0/16 citations) and share three high-weight clinical errors. DeepSeek Fast is materially stronger for Chinese clinician-facing tasks and should be preferred where an LLM is used at all — always under clinician supervision.

> Full method, limitations, and the verbatim prompt are in `../preprint/clinical_benchmark_preprint.md` and `../framework.md`.
