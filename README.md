# Brand Transformation in European Politics: Replication Guide

**Repository:** Replication materials for  
**Endre Borbáth & Swen Hutter (forthcoming).** *Brand Transformation in European Politics: The Rise and Limits of Nonclassical Names*, **Perspectives on Politics**.

This README explains what each numbered file does, what it produces (figures/tables), required inputs, and how to replicate the analysis end-to-end.

---

## Quick start

1. **Software**: R (≥ 4.2 recommended) with RMarkdown.  
2. **Clone** the repo and keep the default folder structure (see “Data & folders”).  
3. **Install packages** used across steps (see below).  
4. **Run in order**: `step1_...Rmd` → … → `step8_...Rmd`. Knit each file; outputs and intermediate data will be written automatically.

---

## Data & folders expected

The scripts assume a project root with these subfolders:

```
primary_data/
  └─ hand_coded_party_name.csv          # manual coding of party names
context_data/
  ├─ MPDataset_MPDS2023a_stata14.dta    # CMP/Manifesto Project
  ├─ idea_export_voter_turnout_database_region.xlsx
  ├─ qog_std_ts_jan24.csv               # QoG time-series
survey_data/
  ├─ AU_survey.Rdata
  ├─ DE_survey.Rdata
  └─ HU_IT_survey.Rdata
```

Intermediate dataset (built by the scripts):

```
dataset_long.Rdata                      # main analysis panel (created in Step 1/2)
```

Paths are handled with `here::here()` inside the Rmds.

---

## Package dependencies (core)

Commonly used packages include: `tidyverse`, `dplyr`, `tidyr`, `forcats`, `stringr`, `lubridate`, `here`, `readxl`, `haven`, `countrycode`, `vdemdata`, `ggplot2`, `ggrepel`, `cowplot`, `kableExtra`, `DiagrammeR`, `corrplot`, `fixest`, `lme4`, `plm`, `effects`, `parameters`, `performance`, `broom.mixed`, `texreg`, `thematic`, `sjPlot`, `sandwich`, `lmtest`, `cregg`, `sparkline`.  
Install any missing packages before running.

---

## What each step does & what it produces

Follow the numbering from the filenames; run them in sequence.

### 1) `step1_building.Rmd` — Build the longitudinal party panel
- **Inputs:** `primary_data/hand_coded_party_name.csv` (+ external sources via packages).
- **What it does:** Constructs a year–party panel, fills gaps (elections/cabinets), merges core identifiers, creates party-level variables (e.g., new party flags, families), and prepares the base structure for analysis.
- **Output (data):** `dataset_long.Rdata` (first build of the master panel).
- **Use this when:** You need to rebuild the base dataset from raw party-name coding.

### 2) `step2_merge_context.Rmd` — Merge context & macro indicators
- **Inputs:** `dataset_long.Rdata`, `context_data/MPDataset_MPDS2023a_stata14.dta`, `context_data/idea_export_voter_turnout_database_region.xlsx`, `context_data/qog_std_ts_jan24.csv`.
- **What it does:** Enriches the panel with CMP/MPDS content, turnout, QoG, volatility, V-Dem (via `vdemdata`), etc.
- **Output (data):** Updated `dataset_long.Rdata` with contextual variables.
- **Use this when:** You need the fully enriched analysis dataset.

### 3) `step3_descriptive_analysis.Rmd` — Descriptive statistics (all Europe)
- **Inputs:** `dataset_long.Rdata`.
- **What it does:** Produces main descriptive figures and summary tables used in the paper’s text and appendix.
- **Key figures/tables generated (indicative headings):**
  - **Figures:**  
    - Fig. 1: Distribution of party names over time (1945–2023)  
    - Fig. 2: Distribution of party name types in Europe  
    - Fig. 3: Distribution of party names by party family (1945–2023)  
    - Variable correlations & country-over-time distributions
  - **Tables:**  
    - Table 2: Distribution of brands by party type  
    - Additional summary counts supporting Fig./Table text
- **Use this when:** You need the pan-European descriptive visuals.

### 4) `step4_regression_analysis.Rmd` — Baseline models (Europe-wide)
- **Inputs:** `dataset_long.Rdata`.
- **What it does:** Estimates hierarchical/logistic models explaining nonclassical naming, with robustness (partial sample 1970–2023, added covariates).
- **Key figures/tables generated:**
  - **Figures:**  
    - Fig. 4 & Fig. 8: Logistic regression models of party naming  
    - Fig. 7: Coverage of V-Party variables
  - **Tables:**  
    - Table 2: Hierarchical logistic regression models of party brands (1945–2023)  
    - Table 3: Partial sample (1970–2023) with additional IVs
- **Use this when:** You need main inferential results for naming.

### 5) `step5_rebranding_analysis.Rmd` — Re-branding dynamics
- **Inputs:** `dataset_long.Rdata`.
- **What it does:** Describes/estimates overall and type-specific party re-branding.
- **Key figures/tables generated:**
  - **Figures:**  
    - Fig. 2: Re-branding over time (1945–2023)  
    - Fig. 3: Re-branding by party family  
    - Fig. 4–5: Logistic regression models (overall and type-specific)
  - **Tables:**  
    - Table 1: Overall re-branding (hierarchical logistic)  
    - Table 2: Re-branding by specific types (hierarchical logistic)
- **Use this when:** You need re-branding descriptives and models.

### 6) `step6_descriptive_analysis_by_region.Rmd` — Descriptives by region
- **Inputs:** `dataset_long.Rdata`.
- **What it does:** Splits descriptives for **Western** vs **Eastern** Europe.
- **Key figures/tables generated:**
  - **Figures:**  
    - Western (a): Time trends, regional distributions, by family  
    - Eastern (b): Time trends, regional distributions, by family
  - **Tables:**  
    - Table 1: Distribution of brands in Western Europe  
    - Table 2: Distribution of brands in Eastern Europe
- **Use this when:** You need region-specific descriptive evidence.

### 7) `step7_regression_analysis_by_region.Rmd` — Models by region
- **Inputs:** `dataset_long.Rdata`.
- **What it does:** Runs the baseline naming models separately for **Western** and **Eastern** Europe.
- **Key figures/tables generated:**
  - **Figures:**  
    - Fig. 4: Logistic regression — Western Europe  
    - Fig. 5: Logistic regression — Eastern Europe
  - **Tables:**  
    - Table 3: Logistic regression — Western Europe  
    - Table 4: Logistic regression — Eastern Europe
- **Use this when:** You need regional heterogeneity in model results.

### 8) `step8_experiment_analysis.Rmd` — Conjoint experiment analyses
- **Inputs:** `survey_data/AU_survey.Rdata`, `survey_data/DE_survey.Rdata`, `survey_data/HU_IT_survey.Rdata`.
- **What it does:** Analyzes conjoint experiments on **new party branding** and **party re-branding**, including heterogeneous effects and country-specific results.
- **Key figures generated (selection by section headings):**
  - **Main text:** Fig. 5 — New party branding conjoint experiment.
  - **Appendix D:** Fig. 2 — Parties re-branding conjoint experiment.
  - **Appendix E:** Extensive set (Figs. 1–31) covering:
    - Continuous-DV versions (new/re-branding)  
    - Country panels: Austria, Italy, Hungary, Germany  
    - Heterogeneity by satisfaction with democracy, left-right, participation, internal/external efficacy, populist attitudes, trust, salience, partisanship.
- **Use this when:** You need experimental evidence and subgroup analyses.

---

## Reproduction tips

- **Order matters:** Always (re)build `dataset_long.Rdata` via **Step 1** and then **Step 2** before running Steps 3–7. The experiment (Step 8) is independent of the panel build but depends on the `survey_data/` files.
- **Project root:** Open the R project at the repo root so `here::here()` resolves relative paths correctly.
- **Figures & tables:** Plots/tables are created within each step’s Rmd (via `ggplot2`, `kableExtra`, `texreg`/`sjPlot`, etc.). Many figures are saved implicitly by the Rmd knitting; names and exact paths follow the defaults in the chunks. Main text and appendix references in the headings map outputs back to the paper.
- **Randomness:** If any models use simulation/bootstrap, set a seed at the top of the file for exact replication.
- **Session info:** For full provenance, keep `sessionInfo()` when knitting.

---

## Citation

If you use or adapt these materials, please cite the paper:

> Borbáth, E., & Hutter, S. (forthcoming). *Brand Transformation in European Politics: The Rise and Limits of Nonclassical Names*. **Perspectives on Politics**.

---

## Contact

For questions about the replication materials, please open an issue on the repository or contact the authors.
