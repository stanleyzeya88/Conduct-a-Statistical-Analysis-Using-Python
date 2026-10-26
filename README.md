# MSc Capstone Project #2: Data and Statistical Reasoning — Consumer Spending Analysis

**Author:** Aung Ze Ya  
**Course:** MSc Capstone / AI Programming Foundations  
**Dataset:** State-Level Consumer Spending Index (`ecommerce_spending.csv`)  
**Data Source:** Opportunity Insights Economic Tracker / Data.gov (2020–2024)

---

## 📌 Project Overview

This repository contains **Project #2 (Data and Statistical Reasoning)** for the MSc Capstone curriculum. The primary analytical objective is to investigate state-level daily consumer spending behavior across five Northeastern US states—**Connecticut (CT), Massachusetts (MA), New Jersey (NJ), New York (NY), and Rhode Island (RI)**—spanning **January 13, 2020 through June 16, 2024** (4,905 daily observations).

Following the **Initial Data Analysis (IDA)** framework proposed by **Huebner et al. (2018)**, this project executes rigorous data hygiene, structural validation, exploratory visualization, assumption checking, and formal inferential hypothesis testing (One-Way ANOVA, Welch's ANOVA, and Tukey HSD post-hoc analysis).

---

## 📁 Repository Structure

```text
capstone-proj2/
├── analysis.ipynb           # Primary Jupyter Notebook containing data pipeline, EDA, and statistical tests
├── ecommerce_spending.csv   # Raw dataset (4,905 rows x 12 columns)
├── module_summary.pdf       # Formal APA-formatted Statistical Analysis Report
├── requirements.txt         # Pinned Python package dependencies for exact environment replication
└── README.md                # Project documentation and reproduction guide
```

---

## 📊 Dataset Description

The dataset `ecommerce_spending.csv` is sourced from Opportunity Insights via Data.gov and records seasonally adjusted credit and debit card transaction indices benchmarked against a pre-2020 baseline period.

* **Observations:** 4,905 daily records (981 records per state, balanced 20% allocation).
* **Time Horizon:** January 13, 2020 – June 16, 2024 (~4.5 years).
* **Key Variables:**
  * `state_name` / `fips`: State identifier (CT [9], MA [25], NJ [34], NY [36], RI [44]).
  * `retail_inc_grocery`: Total retail spending index including grocery (Primary Dependent Variable).
  * `grocery_spending`: Grocery and food store transaction index.
  * `food_service_spending`: Accommodation and food services transaction index.
  * `apparel_gen_spending`, `recreation_spending`, `healthcare_spending`, `transportation_spending`: Additional merchant category indices.
* **Data Quality:** 0 missing values across all 12 columns.

---

## 🔬 Methodology & Statistical Framework

1. **Initial Data Analysis (IDA):** Data ingestion, column standardization into `snake_case`, FIPS code mapping, and data hygiene checks following Huebner et al. (2018).
2. **Descriptive Statistics:** Grouped central tendency (mean, median) and dispersion (std, IQR) calculated by state to capture between-group heterogeneity.
3. **Exploratory Visual Models:**
   * **Figure 1 (Box Plot):** Retail spending distribution by state (Primary visual model reflecting group shifts).
   * **Figure 2 (Correlation Heatmap):** Co-movement matrix across merchant categories (r = +0.82 for general merchandise/apparel).
   * **Figure 3 (Scatter Plot):** Grocery vs. food service spending interaction highlighting spatial clustering.
4. **Hypothesis Testing:**
   * **Null Hypothesis (H0):** Mean daily retail spending is equal across all five states.
   * **Alternative Hypothesis (H1):** At least one state mean daily retail spending index differs significantly.
   * **Assumption Checks:** Normality supported via the Central Limit Theorem (N = 4,905). Homogeneity of variance evaluated via **Levene's Test** (W = 33.51, p < 0.001).
   * **Inferential Models:** **One-Way ANOVA** and heteroscedasticity-robust **Welch's ANOVA** (Delacre et al., 2019).
   * **Post-Hoc Analysis:** Pairwise **Tukey HSD** test mapping state-level differences.

---

## 📈 Key Findings & Results

| Statistical Test | Test Statistic | p-value | Decision (alpha = 0.05) | Effect Size (eta_p^2) |
| :--- | :---: | :---: | :---: | :---: |
| **Standard One-Way ANOVA** | F(4, 4900) = 22.49 | 1.99 x 10^-18 | Reject H0 | 0.018 (Small–Moderate) |
| **Welch's ANOVA** | F_Welch(4, 2441.13) = 23.11 | 9.09 x 10^-19 | Reject H0 | 0.018 |

### Post-Hoc Tukey HSD Tier Structure:
* **High Spending Tier:** Massachusetts (mean = 22.21) and New Jersey (mean = 21.17) — statistically indistinguishable (p = 0.264).
* **Low Spending Tier:** New York (mean = 18.90) and Rhode Island (mean = 17.95) — statistically indistinguishable (p = 0.348).
* **Intermediate Tier:** Connecticut (mean = 19.35) — differs significantly from MA (p < 0.001) and NJ (p = 0.004), but not from NY (p = 0.907) or RI (p = 0.052).

---

## ⚠️ Limitations & Bias Analysis

1. **Card-Transaction Proxy Bias:** Aggregated credit/debit card feeds underrepresent cash-dominant transactions, informal economic activity, and unbanked populations.
2. **Relative Indexing:** Values reflect percentage change relative to a pre-2020 baseline, not absolute dollar volumes.
3. **Geographic Scope:** Findings from five dense Northeastern states do not generalize to Southern, Midwestern, or rural economies.
4. **Ecological Fallacy:** Macro state-level aggregations mask microeconomic variation between urban hubs (NYC, Boston) and rural counties.

---

## 💻 Environment Setup & Reproduction Guide

To recreate the analysis environment and run `analysis.ipynb` top-to-bottom:

### 1. Set Up Virtual Environment
```bash
python -m venv capstone-proj2
source capstone-proj2/bin/activate  # On Windows: capstone-proj2\\Scripts\\activate
```

### 2. Install Pinned Dependencies
```bash
pip install -r requirements.txt
```

### 3. Launch Jupyter Notebook
```bash
jupyter notebook analysis.ipynb
```

---

## 📚 References & Scholarly Citations

* **Delacre, M., Lakens, D., & Leys, C. (2019).** Why psychologists should by default use Welch's t-test instead of Student's t-test. *International Review of Social Psychology*, 30(1), 92–101.
* **Field, A. (2013).** *Discovering statistics using IBM SPSS statistics* (4th ed.). SAGE Publications.
* **Harris, C. R., et al. (2020).** Array programming with NumPy. *Nature*, 585(7825), 357–362.
* **Huebner, M., et al. (2018).** Initial data analysis for longitudinal studies to build a solid foundation for reproducible analysis. *PLOS ONE*, 13(9), e0204681.
* **Kim, T. K. (2017).** Understanding one-way ANOVA using conceptual figures. *Korean Journal of Anesthesiology*, 70(1), 22–26.
* **McKinney, W. (2010).** Data structures for statistical computing in Python. *Proceedings of the 9th Python in Science Conference*, 51–56.
* **Pineau, J., et al. (2021).** Improving reproducibility in machine learning research. *Journal of Machine Learning Research*, 22(164), 1–20.
