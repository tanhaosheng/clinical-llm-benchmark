# A Clinician-Authored Benchmark of Free-Tier Chinese Large Language Models on Breast-Cancer Adjuvant-Decision Reasoning Against the 2026 Chinese Breast Cancer Society (CBCS) Guideline

**Tan Haosheng, MD, PhD**¹

¹ Department of Thyroid and Breast Surgery, Taizhou People's Hospital, Taizhou, Jiangsu, China

Correspondence: Tan Haosheng (tanhaosheng@tanhaosheng.asia)

**Preprint** — not peer-reviewed. This manuscript is distributed as a preprint and has not been certified by peer review.

---

## Abstract

**Background.** Free-tier large language models (LLMs) are increasingly used by clinicians for decision support, yet their reliability on guideline-concordant oncology reasoning is poorly quantified, especially for Chinese-language guidelines. We present a reproducible, clinician-designed benchmark evaluating two free-tier Chinese LLMs on a de-identified post-operative breast-cancer case requiring adjuvant-therapy reasoning anchored to the 2026 Chinese Breast Cancer Society (CBCS) guideline.

**Methods.** A single de-identified case (post-mastectomy, pTis/pT1mi ambiguity, Luminal A-like) was presented to (A) DeepSeek web "Fast mode" and (B) Zhipu ChatGLM 5.2 web, each run three times (free tier, zero cost). A 16-item, 100-point scoring rubric with guideline-section citation requirements, weighted by clinical impact, was applied item-by-item. Stability was defined as max−min ≥ 8 points triggering an "unstable" flag.

**Results.** DeepSeek scored 28/28/28 (median 28/100; stability 0; ~3–4 s/run; guideline-section citation accuracy 0/16). ChatGLM scored 10/2/5 (median 5/100; spread 8 → unstable; ~130 words/run; all three answers in English despite a Chinese prompt; citation accuracy 0/16). Both models committed three high-weight failures: (1) accepting the discordant "TisN0M0" discharge stage without questioning the invasion foci; (2) failing to downgrade endocrine recommendation for post-mastectomy DCIS to "consider/optional"; (3) omitting the ≥60-year age cutoff governing aromatase-inhibitor vs tamoxifen choice. DeepSeek outperformed ChatGLM on every comparable dimension and produced Chinese-output, verifiable reasoning.

**Conclusions.** Neither free-tier model is safe for standalone clinical use; both lack transparent guideline grounding. DeepSeek Fast mode provides higher-density, reproducible Chinese reasoning and is preferable for Chinese clinician-facing tasks, but must remain clinician-supervised. We release the open framework (prompt + rubric) to enable replication.

**Keywords:** large language models; clinical decision support; breast neoplasms; clinical practice guidelines; benchmark; AI for surgeons.

---

## 1. Background

Large language models are being adopted by physicians for rapid information retrieval, draft documentation, and decision exploration. In surgical oncology, where guideline concordance is both legally and prognostically consequential, the risk of confident-but-incorrect model output is high. Prior LLM clinical benchmarks have focused on US/European guidelines (e.g., NCCN, ESMO) and English-language prompting. Chinese clinicians operate under national guidelines—such as the *Chinese Breast Cancer Society (CBCS) Diagnosis and Treatment Guideline*, Version 2026.1.0—and routinely use Chinese-language, free-tier models (DeepSeek, ChatGLM). Whether these models reason concordantly with the CBCS guideline, and whether they expose their guideline basis, is unmeasured.

We therefore constructed a clinician-authored benchmark: a single,真实 (de-identified) post-operative breast-cancer case demanding structured adjuvant-decision reasoning, scored against the 2026 CBCS guideline using a transparent 16-item rubric. The goal is not to endorse any model for patient care, but to quantify failure modes relevant to safe clinical use and to provide a replicable evaluation method.

## 2. Methods

### 2.1 Case vignette (de-identified)

A 60-year-old postmenopausal female, one day after right radical breast surgery, presented for review. Pathology: right breast specimen consistent with invasive carcinoma dominated by low-grade ductal carcinoma in situ (DCIS) with intraductal papillary carcinoma; largest tumor diameter 0.6 cm; three stromal invasion clusters measured ~0.05, 0.06, and 0.2 cm; no lymphovascular or perineural invasion; margins and axilla free. Right sentinel node (0/2) and perisentinel node (1) negative. Left breast mass: adenosis with fibroadenoma. Immunohistochemistry: ER 3+ (90%), PR 3+ (90%), HER-2 (0), Ki-67 5%, P53 wild-type, EGFR (−). Discharge diagnosis: right breast malignancy, pTNM **TisN0M0 (Stage 0)**.

The case was deliberately chosen for high discrimination: the pathology describes stromal invasion (invasive carcinoma) while the discharge label is "Tis," and the 60-year age sits exactly on the aromatase-inhibitor/tamoxifen cutoff.

### 2.2 Reference standard

The 2026 CBCS Breast Cancer Diagnosis & Treatment Guideline (Essence Edition, Version 2026.1.0) was the sole reference standard. Where the guideline is silent, models were expected to state "guideline silent" and provide clinical reasoning.

### 2.3 Models under test

| Model | Interface | Tier | Input |
|---|---|---|---|
| DeepSeek (Fast mode) | chat.deepseek.com | Free | Text (Expert mode lacks image input) |
| Zhipu ChatGLM 5.2 | chatglm.cn | Free | Image (screenshot of de-identified record) |

Both were used at zero monetary cost. DeepSeek was evaluated on text input because its Expert mode did not accept the image; ChatGLM received the image. This asymmetry is a stated limitation (Section 4.5).

### 2.4 Prompt and task specification

Both models received an identical standardized prompt instructing them to act as a clinical-decision assistant for a Chinese surgeon, to reason strictly from the 2026 CBCS guideline (not earlier or foreign versions), to structure output with bullet points, and to cite specific guideline sections/pages. The task required, in order: (1) pathology re-interpretation and stage correction; (2) local-therapy review; (3) systemic adjuvant therapy (chemo, endocrine, anti-HER2); (4) safety and follow-up; (5) explicit self-assessment of confidence and uncertainty. The full prompt is reproduced in the Appendix.

### 2.5 Scoring rubric (max 100)

Each item is weighted by clinical impact; sub-items scored 0/1/2 (2 = fully correct + cites guideline section; 1 = directionally correct but missing detail/citation; 0 = wrong/omitted). A correct item that cites no specific CBCS section is capped at 1, because guideline grounding cannot be verified.

| # | Item | Max |
|---|---|---|
| 1.1 | Accept TisN0M0? (should question ambiguity) | 6 |
| 1.2 | Stage correction (T1a vs T1mi, multifocal rule) | 10 |
| 1.3 | Molecular subtype (Luminal A-like) | 4 |
| 2.1 | Surgery rationale + ALND need | 8 |
| 2.2 | Adjuvant radiotherapy indication | 4 |
| 3.1 | Chemo indication + multigene (Oncotype DX) | 10 |
| 3.2a | Endocrine necessity + mastectomy/BCS difference **(core)** | 12 |
| 3.2b | AI vs TAM + age cutoff **(core)** | 10 |
| 3.2c | Drug dose & duration | 6 |
| 3.2d | OFS / extension / CDK4/6 | 6 |
| 3.3 | Anti-HER2 indication | 4 |
| 4.1 | Endocrine adverse-event monitoring | 6 |
| 4.2 | Bone density & lifestyle | 4 |
| 4.3 | Follow-up plan (first 5 years) | 4 |
| 4.4 | Contralateral breast + BRCA testing | 4 |
| 5 | Self-assessment + uncertainty expression | 2 |
| **Total** | | **100** |

### 2.6 Evaluation procedure

Each model was run three times with identical prompt and unchanged context; date/time, model version, response time, and any "web search" hint were recorded. The rubric was applied item-by-item against the full text of each answer (not truncated screenshots). Stability criterion: max−min ≥ 8 points → flagged "unstable."

### 2.7 Ethical and safety framing

All patient data were de-identified; no re-identifying fields were included. The benchmark is an internal LLM-selection evaluation and **does not constitute clinical advice**; model output must not be used for real patient decisions.

## 3. Results

### 3.1 Overall performance

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

### 3.2 Item-level scorecard (median points)

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

### 3.3 DeepSeek: three systematic failures (all three runs)

1. **Never questions staging (items 1.1+1.2, 16 pts lost).** Pathology states "3 stromal invasion clusters, largest 0.2 cm = 2 mm." Microinvasion is a single focus ≤1 mm; 0.2 cm already exceeds it → at least pT1a (Stage IA). All runs copied "TisN0M0 Stage 0" without flagging the ambiguity—a safety-level error, since staging mismatch cascades into treatment intensity and follow-up.
2. **Post-mastectomy DCIS endocrine not downgraded (item 3.2a, 12 pts lost).** CBCS P59 note a: for DCIS after mastectomy, endocrine drugs belong to *chemoprevention*, recommendation downgraded to "consider/optional." All runs applied the "DCIS → endocrine strongly recommended" template without distinguishing mastectomy vs breast-conserving surgery—the highest-discrimination item.
3. **60-year AI/TAM cutoff omitted (item 3.2b, 10 pts lost).** CBCS P59 note b: AI's advantage over tamoxifen is mainly in postmenopausal women **<60**; at ≥60 the two are near-equivalent. The patient is exactly 60. Runs gave "AI first choice" without writing the cutoff, showing no fine reading of the guideline.

*Strengths:* correct chemo-exemption (Run 1 also proactively raised Oncotype DX); Run 3 correctly noted routine tumor markers not recommended; mentioned AI bone/lipid monitoring; perfectly reproducible (zero variance).

### 3.4 ChatGLM: two independent critical flaws

1. **All-English output (usability failure).** The prompt and case were Chinese, yet all three answers were English—near-zero usability for Chinese clinicians and indicating the model did not absorb the Chinese medical context. Clinically unacceptable regardless of score.
2. **Very low information density + instability (quality failure).** ~130 words/run (DeepSeek ~450), almost no concrete decisions; Run 2 scored 2 (essentially restating the case + "let the doctor decide"). Spread = 8 triggered the instability threshold—repeating the question yields unpredictable results.

### 3.5 Head-to-head comparison

DeepSeek Fast ≫ ChatGLM 5.2 on every comparable dimension: higher score (28 vs 5 median), perfect stability (0 vs 8), Chinese output, ~3× information density, and correct chemo-exemption with Oncotype DX mention. Both failed the three core items and both achieved 0/16 guideline-citation accuracy. ChatGLM's only relative advantage—English output—is irrelevant to the Chinese clinical task and untested for international guidelines here.

## 4. Discussion

### 4.1 Guideline-citation transparency is the dominant gap

Both models scored 0/16 on citing specific CBCS sections. A clinician cannot verify whether an answer derives from the actual guideline or from generic training knowledge. For YMYL (Your-Money-Your-Life) medical content, unverifiable grounding is the central safety defect—and the reason neither model may be trusted alone.

### 4.2 Clinical safety implications

The shared failure to question a discharge stage discordant with pathology (Tis vs invasion) is the most consequential. A model that "confidently" accepts an incorrect stage will propagate errors into treatment and follow-up recommendations. Our framework makes this failure explicit and scorable, which generic chatbot use does not.

### 4.3 Why DeepSeek outperformed

DeepSeek produced higher-density, reproducible, Chinese-language reasoning with correct high-level judgments (no chemo, follow-up cadence). ChatGLM's English output and instability suggest weaker instruction-following on Chinese clinical prompts. Neither reached a threshold for standalone trust, but DeepSeek at least yields a "wrong-but-deep" chain a clinician can verify.

### 4.4 Framework generalizability

The method (standardized prompt + weighted rubric + stability protocol + open replication) generalizes to other cases, stages, subtypes, and models. Expanding to ≥5 cases would strengthen comparative claims. We release the framework openly (Section 5) so others can reproduce or extend it.

### 4.5 Limitations

(1) Single case; (2) free tier only; (3) input-modality asymmetry—DeepSeek on text, ChatGLM on image—means visual/OCR limitations may contribute to ChatGLM's errors and the comparison is not perfectly controlled; (4) scores reflect one clinician's rubric application; (5) the 2026 CBCS guideline version may update. These limit generalizability but do not affect the demonstrated failure modes.

## 5. Conclusions

Free-tier Chinese LLMs are not yet reliable for standalone breast-cancer adjuvant-decision reasoning against the CBCS guideline: both tested models failed to expose guideline grounding (0/16 citations) and.shared three high-weight clinical errors. DeepSeek Fast mode is materially stronger for Chinese clinician-facing tasks and should be preferred where an LLM is used at all—always under clinician supervision. We provide the open benchmark framework to accelerate reproducible evaluation.

## Data and Code Availability

The full framework (prompt, 16-item rubric, answer key), both models' three raw answers, and the item-level scorecards are publicly available at **https://tanhaosheng.asia/clinical-benchmark/**. The evaluation method is released for replication and extension under a permissive license.

## Ethics Statement

This study used a single de-identified case vignette with no personal identifiers and required no institutional review board approval. It is an LLM-evaluation methodology paper and does not involve human-subject research, interventions, or patient care. Model outputs must not be used for clinical decisions.

## Author Contributions

T.H. conceived the benchmark, designed the case and rubric, performed all evaluations, interpreted results, and wrote the manuscript.

## Funding

None.

## Competing Interests

The author operates a public educational website (tanhaosheng.asia) on AI tools for surgeons; no financial relationship with any LLM vendor evaluated herein.

## References

1. Chinese Anti-Cancer Association. *Chinese Breast Cancer Society (CBCS) Diagnosis and Treatment Guideline (Essence Edition)*. Version 2026.1.0. 2026.
2. American Joint Committee on Cancer. *AJCC Cancer Staging Manual*, 8th ed. Chicago: AJCC; 2017.
3. Sparano JA, et al. Adjuvant chemotherapy guided by a 21-gene expression assay in breast cancer. *N Engl J Med*. 2018;379:111–121 (TAILORx).
4. Kalinsky K, et al. Adjuvant chemotherapy guided by a 21-gene assay in breast cancer. *N Engl J Med*. 2021;385:2336–2347 (RxPONDER).
5. Baum M, et al. (ATAC Trialists' Group). Anastrozole alone or in combination with tamoxifen vs tamoxifen alone. *Lancet*. 2002;359:2131–2139.
6. Thurlimann B, et al. (BIG 1-98 Collaborative Group). A comparison of letrozole and tamoxifen. *J Clin Oncol*. 2005;23:719–725.

---

## Appendix: Standardized Prompt (verbatim)

```
You are a clinical-decision assistant serving a Chinese surgeon. Your answer MUST be
strictly based on the 2026 Chinese Anti-Cancer Association Breast Cancer Diagnosis &
Treatment Guideline (CBCS Version 2026.1.0). Do NOT substitute an earlier version or a
foreign guideline. Answer with bullet points and a clear structure, and explicitly state
the guideline basis (section / page / reference number). Where the guideline is silent,
write "guideline silent" and give your own clinical judgment with reasoning.

[Case summary] (de-identified)
Patient: female, 60, retired.
Chief complaint: 1 day after radical right-breast cancer surgery, requesting review.
History: In 2026-04 underwent radical right-breast surgery (simple mastectomy + sentinel
lymph node biopsy).
Post-op pathology:
  - Right breast specimen: invasive carcinoma dominated by low-grade DCIS with
    intraductal papillary carcinoma; largest tumor diameter 0.6 cm;
    slides show 3 clusters of stromal invasion, ~0.05 cm, 0.06 cm, 0.2 cm;
    no definite lymphovascular or perineural invasion; margins and axilla free.
  - Right sentinel node (0/2): negative. Right perisentinel node (1): negative.
  - Left breast mass: adenosis with fibroadenoma.
IHC: ER 3+ (90%), PR 3+ (90%), HER-2 (0), P53 (+, wild-type), Ki-67 (+, 5%), EGFR (−).
Discharge diagnosis: right breast malignancy, pTNM TisN0M0 (Stage 0).

[Task] In order, each item must state its guideline basis:
1. Pathology re-interpretation (accept TisN0M0? stage correction; molecular subtype)
2. Local therapy review (surgery rationale + ALND; adjuvant radiotherapy)
3. Systemic adjuvant therapy (chemo + multigene; endocrine necessity, AI vs TAM + age
   cutoff, dose/duration, OFS/extension/CDK4-6; anti-HER2)
4. Safety & follow-up (AE monitoring; bone density; 5-year plan; contralateral + BRCA)
5. Self-assessment (confidence; points lacking clear 2026 CBCS evidence)
```
