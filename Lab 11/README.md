# Data Wrangling & Engineering Pipeline

## Objective
Engineered a production-ready feature set from a structurally compromised HR economics dataset by diagnosing missingness patterns, resolving multicollinearity, and applying cardinality-reduction techniques to ensure downstream econometric validity.

---

## Methodology

- **Missingness Diagnosis via `missingno`:** Audited the dataset's missing data architecture to classify null patterns as Missing At Random (MAR), distinguishing systematic from stochastic absence and informing imputation strategy accordingly.

- **Targeted Imputation:** Applied theoretically grounded imputation procedures consistent with the identified MAR mechanism, preserving distributional integrity and avoiding the introduction of estimation bias.

- **Dummy Variable Trap Mitigation:** Encoded categorical variables using reference-class dropping — omitting one category per feature during one-hot encoding — to eliminate perfect multicollinearity and ensure full-rank design matrices required for OLS identification.

- **Target Encoding for High-Cardinality Geography:** Compressed high-dimensional geographic variables using target encoding via `category_encoders`, replacing sparse nominal categories with their conditional outcome means to reduce dimensionality while retaining predictive signal.

- **Pipeline Orchestration:** Coordinated all transformation steps using `pandas` and `statsmodels`, maintaining reproducibility and separation of concerns across preprocessing and modeling stages.

---

## Key Findings

The pipeline successfully resolved three canonical data quality threats common to applied econometric work. Missingness was confirmed as MAR, validating the use of conditional imputation without resorting to full-case deletion and its associated sample attrition. The dummy variable trap was preemptively neutralized through systematic reference-class exclusion, producing a full-rank regressor matrix amenable to stable coefficient estimation. High-cardinality geographic data — typically a source of model bloat and overfitting — was compressed into a single continuous feature via target encoding, preserving geographic variation in a statistically tractable form. The resulting dataset is structurally sound and econometrically model-ready.

---

**Stack:** Python · pandas · statsmodels · missingno · category_encoders  
**Data:** `messy_hr_economics.csv`
