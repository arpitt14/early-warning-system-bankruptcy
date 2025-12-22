# Early Warning System for Corporate Financial Distress
### Using Machine Learning and Temporal Evaluation

**Author:** Arpit Thayal  
**Dataset:** Polish Companies Bankruptcy Dataset (UCI)

---

Corporate bankruptcy is rarely a sudden event; instead, it emerges through gradual financial deterioration. This project develops an **Early Warning System (EWS)** for corporate financial distress using financial ratio data and machine learning. Unlike conventional approaches that rely on random train–test splits, this work emphasizes **temporal evaluation**, assessing how early bankruptcy risk can be detected across different time horizons (1–5 years before failure).

Using category-wise exploratory data analysis, principled feature selection, and multiple machine learning models, the study demonstrates that bankruptcy risk is **horizon-dependent**. Linear models capture early structural weaknesses, while tree-based models effectively identify nonlinear crisis-stage dynamics. Random Forest models achieve the strongest overall performance, validating their suitability for early warning applications.

---

## 1. Introduction

Corporate bankruptcy has significant economic and social consequences, affecting employees, investors, and financial institutions. Accurate early detection of financial distress enables proactive intervention, risk mitigation, and informed decision-making.

Traditional bankruptcy prediction models often treat the problem as a static classification task and rely on random train–test splits, which can lead to **information leakage** and misleading performance estimates. In contrast, an effective Early Warning System must answer a more nuanced question:

> *How early can financial distress be detected before bankruptcy occurs?*

This project addresses this question by designing a **time-aware machine learning framework** that evaluates model performance across multiple years before bankruptcy.

---

## 2. Dataset Description

The project uses the **Polish Companies Bankruptcy Dataset** from the UCI Machine Learning Repository.

### Key Characteristics
- Separate datasets corresponding to **1 to 5 years before bankruptcy**
- Each instance represents a company
- Features consist of **financial ratios** derived from balance sheets, income statements, and cash-flow statements
- Target variable:
  - `1` → Bankrupt  
  - `0` → Non-bankrupt  

The dataset is highly imbalanced, reflecting real-world bankruptcy frequencies.

---

## 3. Exploratory Data Analysis (EDA)

Rather than performing superficial EDA on all variables, analysis was conducted **category-wise**, focusing on financially causal dimensions.

### 3.1 Profitability
Profitability ratios revealed that distressed firms exhibit:
- persistent negative or declining profitability
- higher variance compared to healthy firms

### 3.2 Liquidity
Liquidity indicators showed strong early-warning behavior:
- current ratio–based measures frequently dropped below critical thresholds
- negative working capital emerged as a key distress signal

### 3.3 Cash Flow
Cash-flow ratios were the most reliable indicators:
- inability to generate cash relative to liabilities strongly preceded bankruptcy
- negative cash-flow measures were significantly more prevalent among bankrupt firms

These findings confirm that financial distress is **multi-dimensional**, arising from the interaction of profitability, liquidity, and cash-flow deterioration.

---

## 4. Feature Selection

Instead of using all available ratios, a compact and interpretable feature set was constructed using:
- financial intuition,
- EDA insights,
- model-based importance from decision trees.

The final feature set included:
- liquidity indicators,
- cash-flow to debt ratios,
- profitability measures,
- leverage ratios,
- firm size as a control variable.

No aggressive outlier removal or feature engineering was applied, as the dataset already consists of engineered financial ratios and extreme values are economically meaningful.

---

## 5. Modeling Approach

Three machine learning models were implemented and compared.

### 5.1 Logistic Regression
- Used as an interpretable baseline
- Captures early structural risk

### 5.2 Decision Tree
- Captures nonlinear threshold effects
- Serves as a diagnostic model for crisis-stage behavior

### 5.3 Random Forest
- Ensemble of decision trees
- Models complex interactions between financial indicators
- Provides strong generalization and robustness

Class imbalance was addressed using class-weighted loss functions.

---

## 6. Temporal Evaluation Framework

A key methodological contribution of this project is the **temporal evaluation strategy**.

### Evaluation Design
- Models were trained on financial data closest to bankruptcy (Year-1)
- Evaluated on datasets from **1 to 5 years before bankruptcy**

This approach avoids information leakage and mirrors real-world early warning use cases.

---

## 7. Results

### 7.1 ROC-AUC Performance Across Time Horizons

| Years Before Bankruptcy | Logistic Regression | Decision Tree | Random Forest |
|------------------------|--------------------|---------------|---------------|
| 1 | ~0.67 | ~0.78 | **~0.88** |
| 2 | ~0.63 | ~0.67 | ~0.71 |
| 3 | ~0.67 | ~0.71 | ~0.75 |
| 4 | ~0.68 | ~0.74 | ~0.77 |
| 5 | ~0.77 | ~0.81 | **~0.83** |

### 7.2 Key Observations
- Logistic Regression performs better at longer horizons, capturing early structural risk
- Decision Trees improve performance closer to bankruptcy by modeling nonlinear effects
- Random Forest consistently outperforms other models across all horizons

---

## 8. Discussion

The results demonstrate that bankruptcy risk evolves over time and cannot be effectively modeled using a single static approach.

- **Early-stage distress** is characterized by structural weaknesses best captured by linear models
- **Crisis-stage distress** exhibits nonlinear interactions between liquidity collapse, cash-flow stress, and leverage escalation
- Ensemble methods effectively integrate both behaviors

These findings emphasize the importance of **time-aware modeling** in financial risk prediction.

---

## 9. Conclusion

This project developed a principled and interpretable Early Warning System for corporate bankruptcy using financial ratio data and machine learning. By combining category-wise EDA, thoughtful feature selection, and temporal evaluation, the study demonstrates that bankruptcy prediction is fundamentally a **temporal risk assessment problem**.

Random Forest models provide the strongest overall performance, while simpler linear models remain valuable for understanding early structural risk. The results highlight that effective early warning systems must balance predictive power with financial interpretability and methodological rigor.

---

## 10. Limitations and Future Work

Potential extensions include:
- model explainability using SHAP,
- decision-threshold tuning for recall-oriented early warning,
- horizon-aware hybrid modeling strategies,
- testing on datasets from other countries or economic contexts.

---

## References

- UCI Machine Learning Repository: Polish Companies Bankruptcy Dataset  
- Altman, E. I. (1968). *Financial Ratios, Discriminant Analysis and the Prediction of Corporate Bankruptcy*  
- Scikit-learn Documentation
