# Brand Transformation in European Politics: Replication Guide

**Repository:** Replication materials for  
**Endre Borbáth & Swen Hutter (forthcoming).** *Brand Transformation in European Politics: The Rise and Limits of Nonclassical Names*, **Perspectives on Politics**.

This README mirrors the **nested header structure (H1 → H2)** of the R Markdown files so you can quickly find the exact code that produces each **figure** and **table**, and whether it belongs to the **Main Text** or the **Appendix**.

# Quick Start

1. **Software**: R (≥ 4.2 recommended) with RMarkdown.  
2. **Clone** the repo and keep the default folder structure (see **Data & Folders**).  
3. **Install packages** (see **Dependencies**).  
4. **Run in order**: `step1_...Rmd` → … → `step8_...Rmd`. Knit each file.

# Data & Folders

Expected structure at the project root:

```
primary_data/
context_data/
survey_data/
```

Intermediate data created by the pipeline:
```
dataset_long.Rdata   # main analysis panel (created in Step 1/2)
```

Paths are handled with `here::here()` in the Rmds.

# Dependencies

Core packages: `tidyverse`, `dplyr`, `tidyr`, `forcats`, `stringr`, `lubridate`, `here`, `readxl`, `haven`, `countrycode`, `vdemdata`, `ggplot2`, `ggrepel`, `cowplot`, `kableExtra`, `DiagrammeR`, `corrplot`, `fixest`, `lme4`, `plm`, `effects`, `parameters`, `performance`, `broom.mixed`, `texreg`, `thematic`, `sjPlot`, `sandwich`, `lmtest`, `cregg`, `sparkline`.

# Step 1 — Build the longitudinal party panel
*File:* `step1_building.Rmd`  
Builds the party–year panel, merges identifiers, computes party-level flags. **Output:** `dataset_long.Rdata`.

# Step 2 — Merge context & macro indicators
*File:* `step2_merge_context.Rmd`  
Enriches `dataset_long.Rdata` with CMP/MPDS, turnout, QoG, V‑Dem (via `vdemdata`).

# Step 3 — Descriptive analysis (Europe-wide)
*File:* `step3_descriptive_analysis.Rmd`

## Analysis in the main text
- Figure 1: Distribution of party names over time (1945-2023)
- Figure 2: Distribution of party name types in Europe
- Figure 3: Distribution of party names by party family (1945-2023)
- Table 2: Distribution of brands by party type

## Appendix A
- Figure 1: Programmatic references in the names of parties (1945-2023)
- Figure 2: Organizational references in the names of parties (1945-2023)
- Figure 3: Distribution over time of party brands across 28 European countries (1945-2023)
- Figures for the Table 1
- Figure 4: Over time distribution of party brands within countries (1945-2023)
- Corelation plots
  - Figure 6: Correlation between context level predictors
  - Figure 5: Correlation between party level predictors

## Appendix B
- Figure 1: Number of parties re-branding between 1945-2023

## Appendix D
- Figure 1: Crisis of representation in Europe

# Step 4 — Regression analysis (Europe-wide)
*File:* `step4_regression_analysis.Rmd`

## Main text
- Figure 4: Logistic regression model of party naming

## Appendix A
- Figure 7: Coverage of the VParty variables
- Table 2: Hierarchical logistic regression models of party brands (1945-2023)
- Table 3: Partial sample (1970-2023) - hierarchical logistic regression models of party brands with additional independent variables
- Figure 8: Logistic regression model of party naming

# Step 5 — Re-branding analysis
*File:* `step5_rebranding_analysis.Rmd`

## Appendix B
- Figure 2: Distribution over time of re-branding parties across 28 European countries (1945-2023)
- Figure 3: Distribution over party families of re-branding parties across 28 European countries (1945-2023)
- Table 1: Overall re-branding (1945-2023) - hierarchical logistic regression models
- Figure 4: Logistic regression model of parties overall re-branding
- Table 2: Re-branding as specific types (1945-2023) - hierarchical logistic regression models
- Figure 5: Logistic regression model of parties re-branding as specific types

# Step 6 — Descriptive analysis by region
*File:* `step6_descriptive_analysis_by_region.Rmd`

## Appendix C (Western Europe)
- Figure 1: Distribution of party names over time by region (a)
- Figure 2: Distribution of party names by region (a)
- Figure 3: Distribution of party names by party family (a)
- Table 1: Distribution of brands in Western Europe

## Appendix C (Eastern Europe)
- Figure 1: Distribution of party names over time by region (b)
- Figure 2: Distribution of party names by region (b)
- Figure 3: Distribution of party names by party family (b)
- Table 2: Distribution of brands in Eastern Europe

# Step 7 — Regression analysis by region
*File:* `step7_regression_analysis_by_region.Rmd`

## Appendix C (Western Europe)
- Table 3: Logistic regression models of brands in Western Europe
- Figure 4: Logistic regression model of party naming in Western Europe

## Appendix C (Eastern Europe)
- Table 4: Logistic regression models of brands in Eastern Europe
- Figure 5: Logistic regression model of party naming in Eastern Europe

# Step 8 — Conjoint experiment analyses
*File:* `step8_experiment_analysis.Rmd`

## Main text
- Figure 5: New party branding conjoint experiment

## Appendix D
- Figure 2: Parties rebranding conjoint experiment

## Appendix E
- Figure 1: New party branding conjoint experiment - continuous dependent variable
- Figure 2: Parties re-branding conjoint experiment - continuous dependent variable
- Figure 3: Austria: New party branding conjoint experiment
- Figure 4: Italy: New party branding conjoint experiment
- Figure 5: Hungary: New party branding conjoint experiment
- Figure 6: Germany: New party branding conjoint experiment
- Figure 7: Austria: Parties re-branding conjoint experiment
- Figure 8: Italy: Parties re-branding conjoint experiment
- Figure 9: Hungary: Parties re-branding conjoint experiment
- Figure 10: Germany: Parties re-branding conjoint experiment
- Figure 11: Heterogeneous effects by satisfaction with democracy (new party branding)
- Figure 12: Heterogeneous effects by satisfaction with democracy (parties re-branding)
- Figure 13: Heterogeneous effects by left-right (new party branding)
- Figure 14: Heterogeneous effects by left-right (parties re-branding)
- Figure 15: Heterogeneous effects by the strength of party identification (new party branding)
- Figure 16: Heterogeneous effects by the strength of party identification (parties re-branding)
- Figure 17: Heterogeneous effects by participation in demonstrations (new party branding)
- Figure 18: Heterogeneous effects by participation in demonstrations (parties re-branding)
- Figure 19: Heterogeneous effects by internal eﬀicacy (new party branding)
- Figure 20: Heterogeneous effects by internal eﬀicacy (parties re-branding)
- Figure 21: Heterogeneous effects by external eﬀicacy (new party branding)
- Figure 22: Heterogeneous effects by external eﬀicacy (parties re-branding)
- Figure 23: Heterogeneous effects by populist attitudes (new party branding)
- Figure 24: Heterogeneous effects by populist attitudes (parties re-branding)
- Figure 25: Heterogeneous effects by trust (new party branding)
- Figure 26: Heterogeneous effects by trust (parties re-branding)
- Figure 27: Heterogeneous effects by issue salience (new party branding)
- Figure 28: Austria: Heterogeneous effects by partisanship (parties re-branding)
- Figure 29: Italy: Heterogeneous effects by partisanship (parties re-branding)
- Figure 30: Hungary: Heterogeneous effects by partisanship (parties re-branding)
- Figure 31: Germany: Heterogeneous effects by partisanship (parties re-branding)

# Reproduction Tips

- **Order matters:** run **Step 1** → **Step 2** before Steps 3–7; Step 8 is independent of the panel but needs `survey_data/`.  
- **Project root:** open the R project at the repo root so `here::here()` resolves paths correctly.  
- **Randomness:** set a seed at the top of files that use simulation/bootstrap.  
- **Provenance:** keep `sessionInfo()` when knitting.

# Citation

> Borbáth, E., & Hutter, S. (forthcoming). *Brand Transformation in European Politics: The Rise and Limits of Nonclassical Names*. **Perspectives on Politics**.

# Contact

Open an issue on the repository or contact the authors.
