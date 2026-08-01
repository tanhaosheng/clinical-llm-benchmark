# Standardized Prompt — Breast-Cancer Adjuvant-Decision Case

This is the **exact prompt** used in the benchmark. Paste it (verbatim) into any model you want to evaluate. Keep the prompt identical across runs so scores are comparable.

> **Input-mode note (methodology):** In the original run, both models received the *same de-identified case*. DeepSeek Fast mode was evaluated on **text** (its Expert mode did not accept the image); ChatGLM 5.2 received a **screenshot** of the de-identified record. For replication, the text version below is the canonical input. If you test an image-capable model, note the modality asymmetry as a limitation.

## Chinese original (canonical)

```
你是为一位中国外科医生服务的临床决策助手。你的回答必须严格基于
2026 版《中国抗癌协会乳腺癌诊治指南与规范》（CBCS Version 2026.1.0），
不要使用更早版本或国外指南替代。回答时必须分点、结构化、明确写出
指南依据（章节/页码或文献编号），凡指南未明确之处请明确写出"指南未明确"
并给出你的临床判断与理由。

【病例摘要】（已匿名化）

患者：女性，60 岁，退休。
主诉：右乳腺癌根治术后 1 天，要求复查诊治。
现病史：2026-04 在我院行右乳癌根治手术（右乳单纯切除 + 前哨淋巴结活检）。
术后病理：
  - 右乳切除标本：基于 IHE 形态，结合免疫组化，符合以"低级别导管内癌
    合并导管内乳头状癌"为主的浸润性癌；癌肿最大径 0.6 cm；
    切片内见 3 簇间质浸润，范围约 0.05 cm、0.06 cm、0.2 cm；
    未见明确脉管内癌栓及神经侵犯；
    标本乳头、皮肤切缘、基底切缘及腋窝均未见癌累及。
  - 另送"右前哨"淋巴结 (0/2)，未见癌转移。
  - 另送"右前哨旁"淋巴结 1 枚，结合冰冻结果，未见癌转移。
  - 另送"左乳肿块"：乳腺腺病伴纤维腺瘤，局部导管上皮增生，
    管腔内见钙盐沉积；免疫组化示局部导管上皮增生。
免疫组化（重点切片 A 号片）：
  ER 3+ (90%)、PR 3+ (90%)、HER-2 (0)、P53 (+, 野生型)、
  Ki-67 (+, 5%)、EGFR (−)、E-cad (+)。
  CK14/SMA/calponin 证实浸润性癌区域肌上皮缺失（标记对照可靠）。
既往史：无慢性病；无食物/药物过敏史。
术后已予"内分泌治疗"，近日无不适，要求复查。
门诊查体：生命体征平稳；患侧乳腺已切除、胸壁切口瘢痕愈合可；
双侧腋窝未扪及肿大淋巴结。
原出院诊断：右乳腺恶性肿瘤，内侧 pTNM 分期 TisN0M0（0 期）。

【任务】
请你按下列顺序逐项给出书面建议，每项均需写明指南依据：

1. 病理再判读
   1.1 你是否认同出院诊断"TisN0M0（0 期）"？
       提示：注意"3 簇间质浸润最大灶 0.2 cm"是否仍属微浸润
       （微浸润定义：单一浸润灶 ≤ 1 mm）。
   1.2 若分期需修正，请给出更准确的 pT/pN/pM 与分期，
       并说明多灶微浸润如何归入 T 分期。
   1.3 分子分型与增殖指数：判定分子亚型（如 Luminal A-like / B-like）。
2. 局部治疗回顾
   2.1 "右乳单纯切除 + SLNB"对该病例是否合理？是否需补做 ALND？
   2.2 该病例是否需要术后辅助放疗？请写明依据。
3. 系统辅助治疗决策
   3.1 化疗指征评估（请按 2026 CBCS 第 7 章相关决策树给出）；
       是否需要做 21 基因 / Oncotype DX？
   3.2 内分泌治疗：
       (a) 该病例是否需要内分泌治疗？理由？指南对"全乳切除后 DCIS"
           与"浸润性癌"的内分泌推荐有何差异？
       (b) 60 岁绝经后患者，AI 与 TAM 各自的地位？哪个是首选？
           写明指南依据（含年龄切点）。
       (c) 推荐具体药物 + 标准剂量 + 疗程。
       (d) 是否需要联合 OFS / 延长治疗 / CDK4/6 抑制剂？
   3.3 抗 HER2 治疗指征？
4. 安全性与随访
   4.1 所选内分泌药物的主要不良反应、监测项目与频率。
   4.2 骨密度监测与生活方式建议（若选 AI）。
   4.3 影像与肿瘤标志物随访计划（前 5 年）。
   4.4 对侧乳腺与 BRCA 胚系检测建议。
5. 自我评估
   请在最后明确写出：
   - 你对本案把握度（高 / 中 / 低）及原因；
   - 哪些决策点在 2026 CBCS 中没有明确证据，
     你是基于何种临床推理给出的。
```

## English verbatim (for non-Chinese models)

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
