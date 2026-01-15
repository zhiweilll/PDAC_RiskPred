# Pancreatic cancer risk–prediction models based on EHR data

The table below summarises seven recent studies that used longitudinal electronic‐health‑record data to predict pancreatic ductal adenocarcinoma (PDAC) risk.  Each entry lists the prediction tasks (time horizon), model approaches, reported discrimination performance (AUC or AUROC) and any available risk‑stratification results.

### Table 1. Overview of PDAC EHR risk‑prediction models

| Reference (year) | Prediction window(s) | Model type |
|------------------|----------------------|-----------|
| Placido et al., 2023 (Nat Med) | 3, 6, 12, 36, 60 months | Transformer / GRU on ICD trajectories vs non‑sequential baselines |
| Park et al., 2025 (npj Digit Med) | 0–3, 3–6, 6–12, 12–36, 36–60 months | Transformer with LLM‑derived EHR embeddings (multi‑task) |
| Jia et al., 2023 (PRISM, eBioMed) | 6–18 months | PrismNN (neural network) and PrismLR (logistic regression) on federated EHR |
| Appelbaum et al., 2021 (Eur J Cancer) | 180, 270, 365 days | Logistic regression on demographics, diagnoses, labs |
| Multimodal early detection (arXiv 2025) | 6, 9, 12 months before diagnosis | Multimodal model: NCDE for labs + BioGPT embeddings for diagnoses |
| Zheng et al., 2025 (Cell Rep Med) | 0–3, 0–6, 0–12, 0–36, 0–60 months | Transformer‑based sequential model on diagnoses + medications |
| Sharma et al., 2018 (END‑PAC) | Up to 3 years after new‑onset diabetes | Logistic regression risk score (age, weight change, Δglucose) in new‑onset diabetes |


### Table 2. Performance and risk stratification

| Reference | Main AUROC/AUC (example window) | Risk stratification / enrichment |
|-----------|----------------------------------|----------------------------------|
| Placido et al. | ~0.91 (12 m); ~0.88 (36 m) | Top 0.1% highest‑risk had ~100‑fold higher PDAC incidence than baseline |
| Park et al. | 6–12 m: AUROC improved from ~0.60→0.67 (site 1), ~0.82→0.86 (site 2); up to ~0.82–0.89 with 3 m exclusion | Higher PPV (up to ~0.14) vs traditional risk factors (~0.004), indicating strong enrichment |
| Jia (PRISM) et al. | AUC ~0.83 (PrismNN), ~0.80 (PrismLR) for 6–18 m | At chosen threshold, detected ~3.5× more PDAC cases than guideline‑based screening with high specificity |
| Appelbaum et al. | AUC ~0.71 (train), ~0.68 (validation) for 365 d | High‑risk 1.7% of population had 3–5× higher PDAC incidence than baseline |
| Multimodal early‑detection (arXiv 2025) | AUC ~0.74 (6 m), ~0.69 (9 m), ~0.68 (12 m) | No explicit risk‑stratification reported; focus on AUC gain over single‑modality baselines |
| Zheng et al. | AUROC ~0.86 (36 m, 3 m exclusion); 12 m AUROC ~0.90 in some subgroups | Top 1,000 of 1M (~0.1%) had SIR ~115 over 12 m, indicating very strong enrichment |
| Sharma et al. (END‑PAC) | AUC ~0.87 in discovery cohort | Score ≥3: sensitivity 80%, specificity 80%; high‑risk group prevalence from ~0.8%→3.6% (~4.4× enrichment); lowest‑risk组基本无病例 |

**Key observations**

- **Prediction windows vary** markedly across studies—from 6–12 months (Appelbaum, multimodal models) to up to 5 years (Placido, Zheng). Shorter windows often achieve higher AUROCs but capture fewer cases; longer windows require balancing discrimination with lead time.
- **Sequential models** (Transformers/GRUs) that encode **temporal disease trajectories** consistently outperform non‑sequential baselines, with AUROCs approaching 0.90 for 12‑month prediction.
- **Inclusion of additional modalities** (lab results, medications, LLM embeddings) yields **incremental improvements** (0.04–0.07 absolute AUROC gain) and enhances positive predictive value.
- **Risk stratification** is critical: models with moderate AUROC can nevertheless enrich PDAC cases by 3‑ to 5‑fold in high‑risk groups (END‑PAC, Appelbaum, PRISM).
- **Generalizability** remains a challenge; performance declines when models are applied across health systems (e.g., Placido’s Denmark‑trained model AUROC drops from 0.879 to 0.710 on US VA data).

This table can guide comparisons of emerging PDAC risk‑prediction frameworks and highlight the trade‑offs between lead time, model complexity, discrimination and clinical utility.
