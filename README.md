# Early Warning System for Corporate Financial Distress

##  Overview
This project builds an **Early Warning System (EWS)** to predict corporate bankruptcy using financial ratios.  
The goal is not just prediction accuracy, but **understanding *when* financial distress can be detected** before failure.

Using the **Polish Companies Bankruptcy Dataset (UCI)**, the project evaluates multiple machine learning models across **different time horizons (1–5 years before bankruptcy)**.

---

##  Problem Statement
Corporate bankruptcies rarely occur suddenly. Financial distress develops gradually through:
- declining profitability,
- liquidity stress,
- cash-flow deterioration,
- increasing leverage.

The objective of this project is to:
> **Predict bankruptcy and analyze how early warning signals evolve over time.**

---

##  Dataset
- **Source**: UCI Machine Learning Repository  
- **Dataset**: Polish Companies Bankruptcy Dataset  
- **Structure**:
  - Separate datasets for **1 to 5 years before bankruptcy**
  - Each instance contains financial ratios
  - Target variable:
    - `1` → Bankrupt
    - `0` → Healthy

 The dataset is **not uploaded** to this repository.  
Please download it directly from UCI:
https://archive.ics.uci.edu/ml/datasets/Polish+companies+bankruptcy+data

---

##  Exploratory Data Analysis (EDA)
EDA was performed **category-wise**, focusing only on financially causal groups:

- **Profitability** (e.g. net profit / total assets)
- **Liquidity** (e.g. current assets / short-term liabilities)
- **Cash Flow** (e.g. operating cash flow / total liabilities)

Key insights:
- Liquidity and cash-flow ratios show strong early-warning signals
- Working capital sign inversion is a critical risk indicator
- Heavy-tailed distributions are expected and meaningful in bankruptcy data

---

##  Feature Selection
Feature selection was guided by:
- Financial intuition
- Category-wise EDA
- Model-based importance (Decision Tree)

Final feature set (~8 features) includes:
- Liquidity indicators
- Cash-flow to debt ratios
- Profitability measures
- Leverage
- Firm size (control variable)

No aggressive outlier removal or feature engineering was performed, as financial ratios are already engineered features.

---

##  Models Used
Three models were trained and compared:

1. **Logistic Regression**
   - Interpretable baseline
   - Captures structural risk well at longer horizons

2. **Decision Tree**
   - Captures nonlinear crisis-stage effects
   - Useful diagnostic model

3. **Random Forest**
   - Strongest overall performer
   - Captures interactions between liquidity, cash flow, and leverage

Class imbalance was handled using `class_weight='balanced'`.

---

##  Temporal Evaluation (Key Contribution)
Instead of a random train–test split, models were evaluated **temporally**:

- Trained on **Year-1 (closest to bankruptcy)**
- Tested on **Year-1 to Year-5**

### Key finding:
- **Logistic Regression** performs better at longer horizons (early structural risk)
- **Tree-based models** dominate near bankruptcy (nonlinear crisis dynamics)
- **Random Forest** performs best across all horizons

This confirms that bankruptcy risk is **horizon-dependent**.

---

##  Results Summary (ROC-AUC)

| Years Before Bankruptcy | Logistic | Decision Tree | Random Forest |
|------------------------|----------|---------------|---------------|
| 1 | ~0.67 | ~0.78 | **~0.88** |
| 2 | ~0.63 | ~0.67 | ~0.71 |
| 3 | ~0.67 | ~0.71 | ~0.75 |
| 4 | ~0.68 | ~0.74 | ~0.77 |
| 5 | ~0.77 | ~0.81 | **~0.83** |

---

##  Conclusion
- Financial distress exhibits **distinct temporal patterns**
- Linear models capture early structural weakness
- Nonlinear models capture crisis-stage dynamics
- Random Forest provides the strongest overall early-warning capability

This project demonstrates the importance of **time-aware evaluation** in financial risk modeling.

---

##  Tech Stack
- Python
- pandas, numpy
- scikit-learn
- matplotlib, seaborn

---

##  Future Work
- SHAP-based explainability
- Threshold tuning for early-warning recall
- Hybrid horizon-aware modeling strategy

---

##  Author
**Arpit Thayal**  

