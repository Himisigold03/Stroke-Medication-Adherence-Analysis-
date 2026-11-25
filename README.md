# Research Data Analysis: Medication Adherence among Stroke Survivors at UITH

I am a data analyst for health research. This repository documents the analysis I carried out for a group research project at the University of Ilorin on **medication adherence and barriers to secondary stroke prevention among stroke survivors at the University of Ilorin Teaching Hospital (UITH)**.

## Contents
1. [About This Work](#1-about-this-work)
2. [Research Questions and Hypotheses](#2-research-questions-and-hypotheses)
3. [Data](#3-data)
4. [Tools](#4-tools)
5. [Data Cleaning](#5-data-cleaning)
6. [Statistical Methods](#6-statistical-methods)
7. [Results](#7-results)
8. [Limitations of the Analysis](#8-limitations-of-the-analysis)
9. [Repository Contents](#9-repository-contents)
10. [Data Privacy](#10-data-privacy)
11. [About Me](#11-about-me)

## 1. About This Work

The research team collected questionnaire data from 45 stroke survivors. My role was the **data analysis**: cleaning the survey data, summarising it, choosing and running the statistical tests, and writing up the results chapter for the project report. The analysis was done in Python (pandas, SciPy, Matplotlib) and written up in the department's report format.

## 2. Research Questions and Hypotheses

1. What is the level of medication adherence among stroke survivors?
2. What barriers do they report?
3. Which factors are associated with adherence?

| Hypothesis | Null statement | Variables tested |
|---|---|---|
| Ho1 | No association between socio-demographic/economic factors and adherence | Age, education, monthly income, drug affordability |
| Ho2 | No association between therapy-related factors and adherence | Medicines per day, treatment duration, side effects |

## 3. Data

- Cross-sectional questionnaire, **N = 45** respondents.
- Sections: socio-demographics, clinical and treatment details, 14 barrier statements (Q19 to Q32), and the 5 MARS-5 items.

**MARS-5 scoring:** Always = 1, Often = 2, Sometimes = 3, Rarely = 4, Never = 5. The five items are summed (range 5 to 25; higher = better adherence).
**Adherence cut-off:** total of 20 or more = adherent; below 20 = non-adherent.

**Barrier scoring:** Strongly Disagree = 1, Disagree = 2, Agree = 3, Strongly Agree = 4. A barrier counts as present when the answer is Agree or Strongly Agree (3 or 4).

## 4. Tools

Python 3, pandas, NumPy, SciPy (`scipy.stats`), Matplotlib, openpyxl, Jupyter Notebook, Microsoft Word (report).

## 5. Data Cleaning

All cleaning was done in code, so the raw file stays untouched.

- Dropped the timestamp, username and collector-name columns.
- Renamed questionnaire headings to short variable names.
- Repaired "medicines per day" answers that Excel had turned into dates (`1 - 2`, `3 - 4`).
- Standardised text (spacing, symbols, spelling) and grouped rare free-text answers into "Other".
- Set "conditions" to "None" where nothing was ticked; grouped free-text "biggest barrier" answers into categories.
- Converted barrier and MARS-5 answers to numeric scores; computed `MARS_Total` and the adherence group.
- Saved raw and clean data as separate sheets (`Raw_Data`, `Clean_Data`).

## 6. Statistical Methods

| Purpose | Method |
|---|---|
| Describe respondents and barriers | Frequencies and percentages |
| Describe MARS-5 total | Mean (SD), median (IQR) |
| Precision of adherence rate | 95% confidence interval for a proportion (`binomtest`) |
| Factor vs adherence | **Fisher's exact test** (2 x 2) |
| Affordability trend | Chi-square test for trend (Cochran-Armitage) with permutation p-value |
| Affordability vs score | Spearman correlation |
| Effect size | Odds ratio with 95% CI (0.5 added to each cell) |

Fisher's exact test was used because most expected counts were below 5. Each factor was collapsed to two groups:

| Factor | Group 1 | Group 2 |
|---|---|---|
| Age | Below 60 | 60 and above |
| Education | Secondary or less | Tertiary |
| Monthly income (N) | Below 71,000 | 71,000 and above |
| Drug affordability | Easy / very easy | Difficult / very difficult |
| Medicines per day | 1 to 4 | 5 or more |
| Treatment duration | Up to 12 months | Over 1 year |
| Side effects | No | Yes |

"Prefer not to say" income answers were excluded from the income test (n = 35). Significance level: p < 0.05.

## 7. Results

**Adherence**

| Measure | Result |
|---|---|
| Adherent | 39 (86.7%), 95% CI 73.2% to 94.9% |
| Non-adherent | 6 (13.3%) |
| MARS-5 total | Mean 22.82 (SD 3.33); median 24 (IQR 22 to 25); range 11 to 25 |

**Top barriers (Agree or Strongly Agree)**

| Barrier | n (%) |
|---|---|
| Not knowing enough about the medicines | 23 (51.1) |
| Transport costly or difficult | 18 (40.0) |
| Medicines too expensive | 17 (37.8) |
| Doctor or pharmacist did not explain | 16 (35.6) |

**Factors vs adherence (Fisher's exact test)**

| Hypothesis | Factor | Group 1: adherent n/N | Group 2: adherent n/N | p-value | Decision |
|---|---|---|---|---|---|
| Ho1 | Age | 25/28 | 14/17 | 0.658 | Fail to reject |
| Ho1 | Education | 19/22 | 20/23 | 1.000 | Fail to reject |
| Ho1 | Monthly income | 17/17 | 15/18 | 0.229 | Fail to reject |
| Ho1 | Drug affordability | 28/33 | 11/12 | 1.000 | Fail to reject |
| Ho2 | Medicines per day | 16/21 | 23/24 | 0.083 | Fail to reject |
| Ho2 | Treatment duration | 26/30 | 13/15 | 1.000 | Fail to reject |
| Ho2 | Side effects | 37/41 | 2/4 | 0.080 | Fail to reject |

**Affordability:** trend chi-square = 1.56, p = 0.212 (exact p = 0.240); Spearman rho = -0.02, p = 0.883; difficult vs easy OR = 0.68 (95% CI 0.10 to 4.66).

No factor was significantly associated with adherence, so Ho1 and Ho2 were not rejected.

## 8. Limitations of the Analysis

- Small sample (n = 45) and only 6 non-adherent respondents, so the tests have low power.
- Collapsing factors into two groups loses detail; seven tests were run without multiple-testing adjustment.
- Adherence is self-reported.
- The adherence rate depends on the cut-off: scores above 20 only would give 37 of 45 (82.2%).

## 9. Repository Contents

```
.
├── README.md
├── notebooks/Stroke_adherence_analysis.ipynb   # cleaning, tables, tests, figures
├── report/Chapter_5_Results.docx               # results chapter I wrote
├── figures/                                    # age distribution, adherence pie chart
└── outputs/Stroke_results_tables.xlsx          # aggregate tables only
```

## 10. Data Privacy

The data are from real patients and are **not published**. Direct identifiers were removed before analysis, and only aggregate tables are shared.

## 11. About Me

I analyse data for health and medical research: survey cleaning, descriptive statistics, hypothesis testing and clear written reporting. I am building a portfolio of research analysis projects, and more will be added here.

GitHub: [Himisigold03](https://github.com/Himisigold03)
