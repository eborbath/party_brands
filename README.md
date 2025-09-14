# Brand Transformation in European Politics: Replication Guide

**Repository:** Replication materials for  
**Endre Borbáth & Swen Hutter (forthcoming).** *Brand Transformation in European Politics: The Rise and Limits of Nonclassical Names*, **Perspectives on Politics**.

This README maps each numbered file to what it produces, and clearly separates **Main Text** and **Appendix** outputs so you can find figures/tables fast.

# Quick Start

1. **Software**: R (≥ 4.2 recommended) with RMarkdown.  
2. **Clone** the repo and keep the default folder structure (see “Data & folders”).  
3. **Install packages** (see Dependencies).  
4. **Run in order**: `step1_...Rmd` → … → `step8_...Rmd`. Knit each file; outputs and intermediate data will be written automatically.

# Data & Folders

Expected structure at the project root:

```
primary_data/
  └─ hand_coded_party_name.csv          # manual coding of party names
context_data/
  ├─ MPDataset_MPDS2023a_stata14.dta    # CMP/Manifesto Project
  ├─ idea_export_voter_turnout_database_region.xlsx
  └─ qog_std_ts_jan24.csv               # QoG time-series
survey_data/
  ├─ AU_survey.Rdata
  ├─ DE_survey.Rdata
  └─ HU_IT_survey.Rdata
```

Intermediate data created by the pipeline:
```
dataset_long.Rdata                      # main analysis panel (created in Step 1/2)
```

Paths are handled with `here::here()` in the Rmds.

# Dependencies

Core packages used across steps: `tidyverse`, `dplyr`, `tidyr`, `forcats`, `stringr`, `lubridate`, `here`, `readxl`, `haven`, `countrycode`, `vdemdata`, `ggplot2`, `ggrepel`, `cowplot`, `kableExtra`, `DiagrammeR`, `corrplot`, `fixest`, `lme4`, `plm`, `effects`, `parameters`, `performance`, `broom.mixed`, `texreg`, `thematic`, `sjPlot`, `sandwich`, `lmtest`, `cregg`, `sparkline`.

Install any missing packages before running.

# Main Text: Figures & Tables Map

- **Step 3 — Descriptive (Europe-wide)**  
  - **Figures:**  
    - Fig. 1 — Distribution of party names over time (1945–2023)  
    - Fig. 2 — Distribution of party name types in Europe  
    - Fig. 3 — Distribution of party names by party family (1945–2023)
  - **Tables:**  
    - Table 2 — Distribution of brands by party type

- **Step 4 — Baseline Regression (Europe-wide)**  
  - **Figures:** Fig. 4 & Fig. 8 — Logistic regression models of party naming; Fig. 7 — V-Party coverage  
  - **Tables:** Table 2 — Hierarchical logistic regression (1945–2023); Table 3 — Partial sample (1970–2023)

- **Step 5 — Re-branding Dynamics**  
  - **Figures:** Fig. 2 — Re-branding over time (1945–2023); Fig. 3 — Re-branding by party family; Fig. 4–5 — Logistic models  
  - **Tables:** Table 1 — Overall re-branding (hierarchical logistic); Table 2 — Type-specific re-branding

- **Step 7 — Models by Region**  
  - **Figures:** Fig. 4 — Western Europe model; Fig. 5 — Eastern Europe model  
  - **Tables:** Table 3 — Western Europe; Table 4 — Eastern Europe

- **Step 8 — Conjoint Experiments**  
  - **Figures:** **Main text Fig. 5** — New party branding conjoint experiment

# Appendix: Figures & Tables Map

- **Step 3 — Additional descriptives**  
  - Variable correlations; country-over-time distributions (appendix figures)

- **Step 4 — Robustness & coverage**  
  - Coverage figures (e.g., V-Party variables)

- **Step 5 — Additional re-branding models**  
  - Extended model variants and type-specific results

- **Step 6 — Descriptives by Region**  
  - **Tables:** Western vs Eastern distributions  
  - **Figures:** Regional time trends; distributions by family

- **Step 7 — Region-specific tables**  
  - Full model tables for Western/Eastern runs

- **Step 8 — Conjoint (Appendix D & E)**  
  - **Appendix D:** Fig. 2 — Parties re-branding conjoint experiment  
  - **Appendix E:** Extensive set (Figs. 1–31), including:  
    - Continuous-DV versions (new/re-branding)  
    - Country panels: Austria, Italy, Hungary, Germany  
    - Heterogeneity by satisfaction with democracy, left-right, participation, internal/external efficacy, populist attitudes, trust, salience, partisanship

# Step-by-Step Pipeline (Run in Order)

## 1) `step1_building.Rmd` — Build the longitudinal party panel
- **Inputs:** `primary_data/hand_coded_party_name.csv` (+ external sources via packages).  
- **What it does:** Constructs a year–party panel, fills gaps, merges core IDs, computes party-level variables, prepares base structure.  
- **Output (data):** `dataset_long.Rdata` (initial build).

## 2) `step2_merge_context.Rmd` — Add context & macro indicators
- **Inputs:** `dataset_long.Rdata`, `context_data/MPDataset_MPDS2023a_stata14.dta`, `context_data/idea_export_voter_turnout_database_region.xlsx`, `context_data/qog_std_ts_jan24.csv`.  
- **What it does:** Enriches with CMP/MPDS content, turnout, QoG, V-Dem (via `vdemdata`).  
- **Output (data):** Updated `dataset_long.Rdata` with contextual variables.

## 3) `step3_descriptive_analysis.Rmd` — Europe-wide descriptives
- **Inputs:** `dataset_long.Rdata`.  
- **Outputs:** Main-text descriptives (Figs. 1–3; Table 2) + appendix descriptives.

## 4) `step4_regression_analysis.Rmd` — Baseline models
- **Inputs:** `dataset_long.Rdata`.  
- **Outputs:** Main-text logistic models (Figs. 4, 7, 8; Tables 2–3) + coverage plots.

## 5) `step5_rebranding_analysis.Rmd` — Re-branding dynamics
- **Inputs:** `dataset_long.Rdata`.  
- **Outputs:** Main-text re-branding figures/tables + appendix model variants.

## 6) `step6_descriptive_analysis_by_region.Rmd` — Region descriptives
- **Inputs:** `dataset_long.Rdata`.  
- **Outputs:** Appendix tables/figures for Western vs Eastern Europe.

## 7) `step7_regression_analysis_by_region.Rmd` — Region models
- **Inputs:** `dataset_long.Rdata`.  
- **Outputs:** Main-text regional figures + appendix model tables.

## 8) `step8_experiment_analysis.Rmd` — Conjoint experiments
- **Inputs:** `survey_data/AU_survey.Rdata`, `survey_data/DE_survey.Rdata`, `survey_data/HU_IT_survey.Rdata`.  
- **Outputs:** Main-text Fig. 5 (new party branding) + Appendix D/E figures and heterogeneity results.

# Reproduction Tips

- **Order matters:** Rebuild `dataset_long.Rdata` via **Step 1** → **Step 2** before Steps 3–7. Step 8 is independent of the panel but needs `survey_data/`.  
- **Project root:** Open the R project at the repo root so `here::here()` resolves paths correctly.  
- **Randomness:** If any models use simulation/bootstrap, set a seed at the top of the file.  
- **Figures & tables:** Created during knitting (e.g., `ggplot2`, `kableExtra`, `texreg`/`sjPlot`). Filenames/paths follow chunk defaults.  
- **Session info:** Keep `sessionInfo()` when knitting for provenance.

# Citation

If you use or adapt these materials, please cite:

> Borbáth, E., & Hutter, S. (forthcoming). *Brand Transformation in European Politics: The Rise and Limits of Nonclassical Names*. **Perspectives on Politics**.

# Contact

For questions about the replication materials, please open an issue on the repository or contact the authors.
