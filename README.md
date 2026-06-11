# NHANES Sleep and Mental Health Biomarker Analysis
## Longitudinal Biological Dataset | CDC/NCHS Real Data | 11,848 US Adults

---

## Overview

Sleep and mental health are commonly discussed together as though the relationship between them is straightforward. This project tests that assumption on real population data rather than accepting it. Using two cycles of the National Health and Nutrition Examination Survey — 2015-16 and 2017-18 — it analyzes how sleep quality, depression severity, and physical biomarkers relate to each other across 11,848 US adults, and whether those relationships held or shifted between the two cycles.

The data comes from the CDC's National Center for Health Statistics. NHANES is one of the most rigorous population health surveys in the world, combining physical examinations, laboratory tests, and standardized questionnaires on the same respondents. Working with it requires handling real-world data challenges: missing values that aren't random, survey design effects, and variables that are coded in ways that reflect clinical measurement rather than clean database conventions.

---

## What the Analysis Found

The most significant finding is a negative one. Sleep duration alone shows no meaningful linear relationship with PHQ-9 depression scores across 9,804 complete cases (r = -0.006, p = 0.52). This challenges the common framing that poor sleep directly predicts depression at the population level. The relationship is more nuanced — in the 18-34 age group the correlation is r = -0.047, p = 0.012, suggesting age modifies the relationship, but the effect is still weak.

What does distinguish depressed from non-depressed adults in this dataset is BMI and alcohol use. Respondents scoring PHQ-9 ≥ 10 had a mean BMI of 31.24 compared to 29.48 in the non-depressed group (p < 0.0001, Cohen's d = 0.228). Average alcohol consumption was 3.11 drinks per day in the depressed group versus 2.58 in the non-depressed group (p < 0.0001). These are statistically significant differences with practically meaningful effect sizes.

The longitudinal comparison between cycles shows population-level biomarker shifts that are small in absolute terms but statistically significant: mean sleep duration declined from 7.74 to 7.64 hours (p = 0.0006), mean systolic blood pressure increased from 124.9 to 126.4 mmHg (p < 0.0001), and mean BMI increased from 29.38 to 29.69 (p = 0.025). Depression scores were unchanged between cycles.

The predictive models achieved a test AUC of 0.5626 with Gradient Boosting — barely above random. This is itself a meaningful result: the features available in this dataset (sleep, BMI, blood pressure, alcohol use, age, gender) do not contain enough discriminative signal to reliably predict individual-level depression risk. That finding has direct implications for what kinds of interventions could plausibly work at population scale.

---

## Data Sources

NHANES 2015-16 (Cycle I) and 2017-18 (Cycle J)
Published by CDC/National Center for Health Statistics
Available at: https://wwwn.cdc.gov/nchs/nhanes/

Modules used:
- DEMO — Demographics (age, gender, race/ethnicity, income, education)
- SLQ — Sleep Disorders (sleep duration, daytime sleepiness)
- DPQ — Depression Screener (PHQ-9, 9-item scale)
- BPX — Blood Pressure (systolic and diastolic, averaged across readings)
- BMX — Body Measures (BMI)
- ALQ — Alcohol Use (average drinks per day)

---

## Key Results

- 11,848 total respondents across 2 survey cycles
- 9,804 complete cases (82.7% completeness)
- Depression prevalence (PHQ-9 ≥ 10): 7.76%
- Mean PHQ-9 score: 3.241
- Mean sleep hours: 7.691
- Sleep-depression correlation: r = -0.006, p = 0.52 (not significant)
- BMI in depressed vs not depressed: 31.24 vs 29.48 (p < 0.0001)
- Alcohol use in depressed vs not: 3.11 vs 2.58 drinks/day (p < 0.0001)
- Systolic BP trend: 124.9 → 126.4 mmHg across cycles (p < 0.0001)
- Sleep duration trend: 7.74 → 7.64 hours across cycles (p = 0.0006)
- Best model AUC: 0.5626 (Gradient Boosting)

---

## How to Run

```bash
# 1. Setup
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# 2. Download NHANES data
# Go to: https://wwwn.cdc.gov/nchs/nhanes/
# Download from 2015-16 (Cycle I) and 2017-18 (Cycle J):
# DEMO, SLQ, DPQ, BPX, BMX, ALQ — Data [XPT] files
# Place in data/ folder with names: DEMO_I.xpt, DEMO_J.xpt, SLQ_I.xpt etc.

# 3. Run full pipeline
python3 main.py

# 4. Skip modeling for faster run
python3 main.py --skip-modeling

# 5. Custom data directory
python3 main.py --data /path/to/xpt/files/
```

---

## Generated Outputs

```
outputs/
├── nhanes_dashboard.png      ← Dashboard with all analytical panels
└── analysis_summary.json     ← Full results with all metrics
```

---



*Built by Raja Palagummi | rajapalagummi.com | github.com/rajapalagummi*
