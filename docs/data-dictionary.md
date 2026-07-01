# Data Dictionary — Naming Conventions Only

This file documents column names and their meanings only. It contains
no actual data, no row values, and no patient information of any kind. Real
datasets are never stored in this repo.

## Main trial dataset (kept local only)

| Column | Meaning |
|---|---|
| PATNO | Unique patient ID (local use only, never shared with AI tools) |
| ARM | Randomized treatment arm |
| AGE | Age at enrollment |
| SEX | Sex |
| PS | Performance status at enrollment (Zubrod/ECOG scale, 0–4) |
| STAGE | Disease stage at enrollment |
| PDL1 | PD-L1 expression status |
| BRAF | BRAF mutation present or not |
| ULCv | Tumor ulceration status |
| RFS | Recurrence-free survival, in days |
| R | 1 = progressed or died, 0 = otherwise |
| SURTIM | Overall survival, in days |
| SURIND | 1 = died, 0 = alive at last contact |

## Medical history dataset (kept local only)

| Column | Meaning |
|---|---|
| PATNO | Unique patient ID (local use only, never shared with AI tools) |
| MHTERM | Free-text medical history term |
| MHONGO | 1 = ongoing, 0 = not ongoing |

## Planned derived columns (comorbidity matrix, to be built)

| Column | Meaning |
|---|---|
| PATNO | Join key back to main dataset (local only) |
| CVD | 1 = cardiovascular disease flag, 0 = none |
| COPD | 1 = COPD/emphysema/chronic bronchitis flag, 0 = none |
| T2D | 1 = type 2 diabetes flag, 0 = none |
| RMD | 1 = rheumatic/musculoskeletal disorder flag, 0 = none |
| N_COMORBID | Count of the above flags that are 1, per patient |
