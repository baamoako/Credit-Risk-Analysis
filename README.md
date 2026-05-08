# Credit Risk Analysis

Statistical analysis of borrower default risk using a 32,581-record loan dataset. Built in R with descriptive statistics, probability modelling, confidence intervals, and hypothesis testing.

---

## What This Project Does

Lenders approve or reject loans based on incomplete information. This analysis quantifies how much that uncertainty costs, specifically: which borrower characteristics correlate with default, how confident we can be in those estimates, and whether the patterns hold under statistical testing.

The dataset covers 12 variables per applicant, including income, employment length, loan grade (A–G), loan purpose, and prior default history.

---

## Key Findings

**Default probability:** 18% of borrowers in this dataset have a prior default on file.

**Age and default:** 79% of borrowers with a default history are between 20 and 30 years old. That's not surprising given shorter credit histories in that cohort, but the concentration is sharper than expected.

**Loan grade risk:** Grade C borrowers showed a 57% conditional probability of default, making them the most concentrated risk segment after controlling for grade.

**Medical loans:** 7% of medical loan applicants defaulted, lower than the dataset average. Medical borrowing may correlate with income stability or urgency-driven repayment behaviour.

**Income (95% CI):** True mean income estimated between $65,402 and $66,748. Standard deviation of $61,983 signals a wide spread; income alone is a weak predictor.

**Grade B proportion (95% CI):** Grade B customers make up 32.1% of the portfolio, with a 95% confidence interval of [31.6%, 32.6%].

**Hypothesis test:** Two-sample t-test found no statistically significant difference in mean loan amounts between applicants with and without a prior default history (p > 0.05). Loan size does not reliably signal default risk in this sample.

---

## Dataset

**Source:** [Credit Risk Dataset](https://www.kaggle.com/datasets/laotse/credit-risk-dataset/data) — L. Tse, 2020  
**Size:** 32,581 observations, 12 variables  
**Missing values handled:** `person_emp_length` (895 NAs), `loan_int_rate` (3,116 NAs)

| Variable | Type | Description |
|---|---|---|
| `person_age` | Discrete numeric | Applicant age |
| `person_income` | Discrete numeric | Annual income |
| `person_home_ownership` | Nominal categorical | RENT / OWN / MORTGAGE |
| `person_emp_length` | Discrete numeric | Employment length (months) |
| `loan_intent` | Nominal categorical | Purpose of loan |
| `loan_grade` | Ordinal categorical | Creditworthiness grade (A–G) |
| `loan_amnt` | Discrete numeric | Loan amount |
| `loan_int_rate` | Continuous numeric | Interest rate |
| `loan_status` | Binary | Default status (0/1) |
| `loan_percent_income` | Continuous numeric | Loan-to-income ratio |
| `cb_person_default_on_file` | Binary categorical | Prior default (Y/N) |
| `cb_person_cred_hist_length` | Discrete numeric | Credit history length (years) |

---

## Methods

**Data preparation:** Categorical variables converted to ordered factors (loan grade A > B > ... > G). Risk tiers created from loan-to-income ratio: Low (≤10%), Medium (≤30%), High (>30%). Age grouped into four bands: 20–30, 31–45, 46–60, 60+.

**Descriptive statistics:** Mean, median, and SD calculated for age, income, and loan amount. The income distribution has a mean/median gap of $11,000, indicating right skew from high earners.

**Probability analysis:** Marginal, joint, and conditional probabilities computed across home ownership, loan intent, loan grade, and age group segments.

**Confidence intervals:** 95% CI for mean income (normal approximation) and for proportion of Grade B customers (proportion z-interval).

**Hypothesis testing:** Two-sample Welch t-test comparing mean loan amounts between default and non-default groups.

---

## Setup

```r
# Clone the repo and set your working directory
setwd("path/to/credit-risk-analysis")

# Load the data
credit_risk <- read.csv("credit_risk_dataset.csv", na.strings = "")

# Run the full analysis
source("credit_risk_analysis.R")
```

**Requirements:** Base R (≥ 4.0). No external packages required.

---

## Repo Structure

```
credit-risk-analysis/
├── credit_risk_analysis.R   # Full analysis script
├── credit_risk_dataset.csv  # Source data
└── README.md
```

---

## Limitations

The hypothesis test used a two-sample t-test without checking for normality in both groups. With 32k observations the CLT makes this defensible, but a non-parametric alternative (Mann-Whitney U) would be more rigorous. Missing values in `loan_int_rate` were dropped rather than imputed, which may bias interest rate-related conclusions.

---

## Author

**Bismark Addo Amoako**  
