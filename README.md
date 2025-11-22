# **Stella Survey: Accent Perception Analysis (R / Quarto)**

This project analyzes **language attitudes toward English accents** using the Stella Survey dataset.
Non-native English speakers rated multiple accent recordings on two perceptual dimensions:

* **Status** (prestige / competence)
* **Solidarity** (friendliness / approachability)

The project includes a full reproducible pipeline:

1. **Data cleaning + reshaping** from raw survey CSV
2. **Exploratory statistical analysis** of hypotheses
3. **Publication-style visualizations and summary tables** in Quarto

---

## 📌 Research Questions & Hypotheses

**H1. Standard vs. Non-standard accents**

* Standard accents will score higher on **status**
* Non-standard accents will score higher on **solidarity**

**H2. Speaker gender effects**

* Male vs female speakers may be rated differently on status/solidarity.

**H3. RP vs GA**

* UK Received Pronunciation (RP) will score higher on **status** than US General American (GA).

---

## 📁 Project Structure

```
/data
  stella_survey.csv
  stella_survey_clean.rds

/scripts
  00_data_cleaning.qmd
  01_analysis.qmd

/figures
  (rendered plots from analysis)
README.md
.gitignore
```

---

## 🔧 Methods Overview

### 1) Data Cleaning & Transformation (`00_data_cleaning.qmd`)

The cleaning script:

* reads the raw CSV (treating `-99` as missing)
* filters for interview-mode participants
* selects participant metadata + rating variables
* reshapes wide → long with `pivot_longer()`
* splits recording IDs into:

  * `recording_id`
  * `country` (UK vs US)
  * `standard` (standard vs non-standard)
  * `speaker_gender`
* recodes participant variables (gender, student status)
* parses numeric years of English instruction
* converts key variables to factors
* saves a tidy dataset as `.rds`

Output:

```
data/stella_survey_clean.rds
```

---

### 2) Analysis & Visualization (`01_analysis.qmd`)

The analysis script:

* loads the cleaned `.rds`
* creates participant-level metadata (deduplicated)
* computes descriptive summaries per hypothesis
* produces plots with `ggplot2` + `viridis` palettes
* formats tables with `flextable` and `kableExtra`
* renders a report to `.docx`

---

## 📈 Key Results (Summary)

### **H1: Standard vs Non-standard**

* **Status:** Standard accents received **higher status ratings** than non-standard accents.
* **Solidarity:** Standard and non-standard accents showed **no meaningful difference**.

**Interpretation:**
Standardness strongly affects perceived prestige, but not perceived warmth.

---

### **H2: Speaker gender**

* **Male speakers** were rated **higher on status**.
* **Female speakers** were rated **higher on solidarity**.

**Interpretation:**
Accent perception is influenced by gendered expectations (authority vs approachability).

---

### **H3: RP (UK) vs GA (US)**

* **UK (RP)** accents scored **higher on status and solidarity** than **US (GA)** accents.

**Interpretation:**
Participants show a consistent preference for UK English across both prestige and affective dimensions.

---

## 👥 Participant Demographics (Context)

* Majority aged **20–26**
* Gender imbalance: **~67% male**, **~33% female**
* Most participants were **not students**
* English instruction clustered around **8 years**
* English contact was polarized (many very low, many high)

These characteristics likely shape the attitude patterns above.

---

## ▶ Reproducibility

### Install packages

```r
install.packages(c(
  "tidyverse", "readr", "knitr", "kableExtra",
  "flextable", "viridis"
))
```

### Run cleaning

Render:

```
scripts/00_data_cleaning.qmd
```

This regenerates the cleaned dataset.

### Run full analysis

Render:

```
scripts/01_analysis.qmd
```

This regenerates all figures and tables.

---

## 🧠 Skills Demonstrated

* **Data cleaning & wrangling** (filtering, selecting, pivoting, recoding)
* **Regex-based metadata extraction** from recording IDs
* **Tidy long-format survey design**
* **Exploratory statistical analysis**
* **Data visualization** (ggplot2, accessible palettes)
* **Publication-ready reporting** (Quarto → Word, flextable)
* **Reproducible workflow structuring**
* **Linguistic interpretation of perceptual data**

---

## 🔒 Data / Ethics Note

The dataset contains **anonymized survey responses** only (age, gender, learning history, ratings).
No personally identifying information is included.

---

## 👤 Author

**Ersin Gültekin**
M.A. Linguistics — University of Freiburg
Computational Linguistics / NLP / Quantitative Linguistics

---
