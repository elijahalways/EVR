# Engineering Visa Research

**Author:** Pok Rui Lai

**Generative AI Declaration Statement:** Generative AI tools were used to assist with the development of this project.

## Acronyms

- **EVR** — Engineering Visa Research
- **NLP** — Natural Language Processing
- **VSRS** — Visa/sponsorship/right-to-work statements
- **fdf** — Filtered DataFrame (Engineering and Internships/Placements)
- **egfdf** — Engineering and Graduate filtered DataFrame
- **efdf** — Engineering filtered DataFrame
- **ipfdf** — Internships/Placements filtered DataFrame
- **gfdf** — Graduate filtered DataFrame
- **ufdf** — Unfiltered DataFrame

## Overview

This repository contains the Python code for the EVR project, implemented using Jupyter Notebooks.

The notebooks are divided into two stages:

1. **Filter** — Processes and filters the raw Adzuna vacancy data
2. **NLP** — Develops and applies machine-learning models to classify VSRS

Notebook names begin with `evr_`, representing **e**ngineering **v**isa **r**esearch.

## Notebooks

### Filter

- **`evr_fdf`** — Produces a **f**iltered **d**ata**f**rame containing vacancies relevant to _engineering_ and _internships/placements_
- **`evr_egfdf`** — Produces a sampled **e**ngineering and **g**raduate **f**iltered **d**ata**f**rame containing vacancies relevant to _engineering_ and _graduates_
- **`evr_efdf`** — Produces a sampled **e**ngineering **f**iltered **d**ata**f**rame containing vacancies relevant to _engineering_
- **`evr_ipfdf`** — Produces a sampled **i**nternships/**p**lacements **f**iltered **d**ata**f**rame containing vacancies relevant to _internships/placements_
- **`evr_gfdf`** — Produces a sampled **g**raduate **f**iltered **d**ata**f**rame containing vacancies relevant to _graduates_
- **`evr_ufdf`** — Produces a sampled **u**n**f**iltered **d**ata**f**rame containing unfiltered vacancy data
- **`evr_filter_visuals`** — Produces visualisations of the filtering results

The sampled datasets contain **12,000 records**, with **1,000 records selected from each quarterly snapshot**. A `random_state` of **42** is used.
`evr_fdf` is not sampled because fewer than 12,000 records remain after filtering.

Please note that only data from `evr_fdf` are directly used in VSRS classification both manually and using NLP.

### NLP

- **`evr_nlp_metrics`** — Trains and evaluates the NLP models
- **`evr_nlp_model`** — Trains the final models and applies them to the remaining unclassified data
- **`evr_nlp_visuals`** — Produces visualisations comparing the NLP models

## Recommended Order

1. `evr_fdf`
2. `evr_egfdf`
3. `evr_efdf`
4. `evr_ipfdf`
5. `evr_gfdf`
6. `evr_ufdf`
7. `evr_filter_visuals`
8. `evr_nlp_metrics`
9. `evr_nlp_model`
10. `evr_nlp_visuals`

## Outputs

This project produces multiple output files including:
- `.pkl` — Trained machine-learning models
- `.csv` — Data files containing processed and/or filtered vacancy datasets
- `.svg` — Vector graphics containing visualisations and figures generated during analysis

Each output file is described below:

### PKL
- `LS1` — single-stage LinearSVC Classification (1) model
- `LS2_1` — dual-stage LinearSVC Relevance (2.1) classification model
- `LS2_2` — dual-stage LinearSVC Legality (2.2) classification model

### CSV
- `[fdf/egfdf/efdf/ipfdf/gfdf/ufdf]_[snapshot_date]` — Data of each filter type for snapshot date (see **Data** section)
- `[fdf/egfdf/efdf/ipfdf/gfdf/ufdf]_all` — Combined data of each filter type
- `[fdf/egfdf/efdf/ipfdf/gfdf/ufdf]_all_vsrs_applied` — Combined data of each filter type with additional VSRS column
- `[fdf/egfdf/efdf/ipfdf/gfdf/ufdf]_all_vsrs_filtered` — Combined data of each filter type containing only rows with VSRS statements
- `vsrs_400` — Randomly shuffled 400 datapoint sample from `fdf_all_vsrs_filtered`
- `vsrs_400_classified` — Manually classified data from `vsrs_400`
- `vsrs_400_relevance` — Manually classified relevance data from `vsrs_400`
- `vsrs_400_legality` — Manually classified legality data from `vsrs_400`
- `vsrs_1240` — Randomly shuffled 1240 datapoint sample from `fdf_all_vsrs_filtered`
- `vsrs_1240_predicted` — NLP-predicted (LS1 + LS2) data from `vsrs_1240`
- `vsrs_1240_comparison` — 3-column extract from `vsrs_1240_predicted` consisting only of VSRS and both classifications (LS1 + LS2)
- `vsrs_1240_difference` — Extract from `vsrs_1240_predicted` consisting only of rows where LS1 and LS2 classifications differ
- `vsrs_1240_comparison_sample` — Randomly shuffled 50 datapoint sample from `vsrs_1240_predicted`
- `vsrs_1640_LS1` — Combined classified dataset of manually-obtained `vsrs_400_classified` and NLP LS1's result from `vsrs_1240_predicted`
- `vsrs_1640_LS2` — Combined classified dataset of manually-obtained `vsrs_400_classified` and NLP LS2's result from `vsrs_1240_predicted`

### SVG
- `fdf_vsrs_line` — line plot of fdf over time
- `filter_pie` — pie chart of VSRS proportion across filter type
- `filter_line` — line plot of VSRS proportion across filter type over time
- `Matrix_LR1` — confusion matrix example of single-stage Logistic Regression for Classification (1)
- `Matrix_LR2_1` — confusion matrix example of dual-stage Logistic Regression for Relevance (2.1)
- `Matrix_LR2_2` — confusion matrix example of dual-stage Logistic Regression Legality (2.2)
- `Matrix_LS1` — confusion matrix example of single-stage LinearSVC for Classification (1)
- `Matrix_LS2_1` — confusion matrix example of dual-stage LinearSVC for Relevance (2.1)
- `Matrix_LS2_2` — confusion matrix example of dual-stage LinearSVC for Legality (2.2)
- `fdf_nlp_pie` — pie chart of classification proportion across LS1 and LS2 models
- `fdf_nlp_line` — line plot of classification proportion across LS1 and LS2 models over time

## Libraries and Environment

The analysis was developed in **Python 3.13.5** using **Jupyter Notebook**.

Required libraries:

- NumPy
- Pandas
- Matplotlib
- scikit-learn
- Joblib

Install the required libraries using:

`pip install numpy pandas matplotlib scikit-learn joblib`

Run the notebooks with the **main repository directory as the working directory**.

## Data

The underlying dataset is licensed and is available only to authorised users.

The required `.dta` files should be placed directly in the **main working directory**, alongside the notebooks.

The analysis uses snapshots from the beginning of each quarter, covering **October 2022 to July 2025**.

The dates in the filenames follow the **`YYYY_MM_DD`** format.

The required snapshots and part files are:

| Snapshot Date | Part files |
|---|---|
| 2022_10_02 | `00000`–`00006` |
| 2023_01_01 | `00002`–`00009` |
| 2023_04_02 | `00000`–`00009` |
| 2023_07_05 | `00000`–`00009` |
| 2023_10_01 | `00000`–`00009` |
| 2024_01_07 | `00000`–`00009` |
| 2024_04_07 | `00000`–`00010` |
| 2024_07_07 | `00000`–`00010` |
| 2024_10_06 | `00000`–`00010` |
| 2025_01_05 | `00000`–`00009` |
| 2025_04_06 | `00000`–`00010` |
| 2025_07_06 | `00000`–`00011` |

The exhaustive list of required `.dta` files is listed below.

```text
output_2022_10_2_part-00000.dta
output_2022_10_2_part-00001.dta
output_2022_10_2_part-00002.dta
output_2022_10_2_part-00003.dta
output_2022_10_2_part-00004.dta
output_2022_10_2_part-00005.dta
output_2022_10_2_part-00006.dta

output_2023_1_1_part-00002.dta
output_2023_1_1_part-00003.dta
output_2023_1_1_part-00004.dta
output_2023_1_1_part-00005.dta
output_2023_1_1_part-00006.dta
output_2023_1_1_part-00007.dta
output_2023_1_1_part-00008.dta
output_2023_1_1_part-00009.dta

output_2023_4_2_part-00000.dta
output_2023_4_2_part-00001.dta
output_2023_4_2_part-00002.dta
output_2023_4_2_part-00003.dta
output_2023_4_2_part-00004.dta
output_2023_4_2_part-00005.dta
output_2023_4_2_part-00006.dta
output_2023_4_2_part-00007.dta
output_2023_4_2_part-00008.dta
output_2023_4_2_part-00009.dta

output_2023_7_5_part-00000.dta
output_2023_7_5_part-00001.dta
output_2023_7_5_part-00002.dta
output_2023_7_5_part-00003.dta
output_2023_7_5_part-00004.dta
output_2023_7_5_part-00005.dta
output_2023_7_5_part-00006.dta
output_2023_7_5_part-00007.dta
output_2023_7_5_part-00008.dta
output_2023_7_5_part-00009.dta

output_2023_10_1_part-00000.dta
output_2023_10_1_part-00001.dta
output_2023_10_1_part-00002.dta
output_2023_10_1_part-00003.dta
output_2023_10_1_part-00004.dta
output_2023_10_1_part-00005.dta
output_2023_10_1_part-00006.dta
output_2023_10_1_part-00007.dta
output_2023_10_1_part-00008.dta
output_2023_10_1_part-00009.dta

output_2024_1_7_part-00000.dta
output_2024_1_7_part-00001.dta
output_2024_1_7_part-00002.dta
output_2024_1_7_part-00003.dta
output_2024_1_7_part-00004.dta
output_2024_1_7_part-00005.dta
output_2024_1_7_part-00006.dta
output_2024_1_7_part-00007.dta
output_2024_1_7_part-00008.dta
output_2024_1_7_part-00009.dta

output_2024_4_7_part-00000.dta
output_2024_4_7_part-00001.dta
output_2024_4_7_part-00002.dta
output_2024_4_7_part-00003.dta
output_2024_4_7_part-00004.dta
output_2024_4_7_part-00005.dta
output_2024_4_7_part-00006.dta
output_2024_4_7_part-00007.dta
output_2024_4_7_part-00008.dta
output_2024_4_7_part-00009.dta
output_2024_4_7_part-00010.dta

output_2024_7_7_part-00000.dta
output_2024_7_7_part-00001.dta
output_2024_7_7_part-00002.dta
output_2024_7_7_part-00003.dta
output_2024_7_7_part-00004.dta
output_2024_7_7_part-00005.dta
output_2024_7_7_part-00006.dta
output_2024_7_7_part-00007.dta
output_2024_7_7_part-00008.dta
output_2024_7_7_part-00009.dta
output_2024_7_7_part-00010.dta

output_2024_10_6_part-00000.dta
output_2024_10_6_part-00001.dta
output_2024_10_6_part-00002.dta
output_2024_10_6_part-00003.dta
output_2024_10_6_part-00004.dta
output_2024_10_6_part-00005.dta
output_2024_10_6_part-00006.dta
output_2024_10_6_part-00007.dta
output_2024_10_6_part-00008.dta
output_2024_10_6_part-00009.dta
output_2024_10_6_part-00010.dta

output_2025_1_5_part-00000.dta
output_2025_1_5_part-00001.dta
output_2025_1_5_part-00002.dta
output_2025_1_5_part-00003.dta
output_2025_1_5_part-00004.dta
output_2025_1_5_part-00005.dta
output_2025_1_5_part-00006.dta
output_2025_1_5_part-00007.dta
output_2025_1_5_part-00008.dta
output_2025_1_5_part-00009.dta

output_2025_4_6_part-00000.dta
output_2025_4_6_part-00001.dta
output_2025_4_6_part-00002.dta
output_2025_4_6_part-00003.dta
output_2025_4_6_part-00004.dta
output_2025_4_6_part-00005.dta
output_2025_4_6_part-00006.dta
output_2025_4_6_part-00007.dta
output_2025_4_6_part-00008.dta
output_2025_4_6_part-00009.dta
output_2025_4_6_part-00010.dta

output_2025_7_6_part-00000.dta
output_2025_7_6_part-00001.dta
output_2025_7_6_part-00002.dta
output_2025_7_6_part-00003.dta
output_2025_7_6_part-00004.dta
output_2025_7_6_part-00005.dta
output_2025_7_6_part-00006.dta
output_2025_7_6_part-00007.dta
output_2025_7_6_part-00008.dta
output_2025_7_6_part-00009.dta
output_2025_7_6_part-00010.dta
output_2025_7_6_part-00011.dta
