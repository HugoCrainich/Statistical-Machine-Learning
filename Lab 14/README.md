# AI Capex Diagnostic Modeling

## Objective

Diagnose and remediate structural estimation failures — specifically heteroscedasticity and multicollinearity — in an OLS regression predicting AI software revenue from capital expenditure and deployment metrics, restoring inferential validity through HC3 robust standard error correction.

---

## Methodology

- **Dataset:** 2026 Nvidia AI Capital Expenditure and Deployment Data, capturing high-variance expenditure tiers characteristic of accelerated AI infrastructure buildout cycles.

- **Baseline OLS Estimation:** Constructed a naive Ordinary Least Squares model in `statsmodels` to establish a performance benchmark and expose latent misspecification.

- **Heteroscedasticity Diagnostics:** Applied the Breusch-Pagan and White tests to formally detect non-constant error variance across capital expenditure tiers. Visualized residual fan-out patterns against fitted values using `matplotlib` and `seaborn` to confirm severe, systematically expanding heteroscedasticity at high-CapEx observations.

- **Multicollinearity Assessment:** Computed Variance Inflation Factors (VIF) across all regressors to identify collinear deployment metrics that could destabilize coefficient estimates and inflate model confidence.

- **Robust Correction — HC3 Estimators:** Re-estimated the model using Heteroscedasticity-Consistent (HC3) robust standard errors via `statsmodels`, a sandwich-type covariance estimator that remains valid under unknown, arbitrary heteroscedasticity without requiring model re-specification.

- **Comparative Inference Analysis:** Conducted a side-by-side comparison of naive OLS vs. HC3-corrected p-values and confidence intervals to quantify the inferential distortion introduced by unaddressed heteroscedasticity.

---

## Key Findings

The naive OLS model exhibited **severe heteroscedasticity** that expanded systematically with capital expenditure magnitude — a pattern consistent with variance scaling in technology deployment environments where high-investment cohorts carry disproportionate outcome uncertainty.

This structural violation caused the baseline model to produce **artificially deflated standard errors**, generating false statistical confidence: several deployment metrics appeared highly significant under naive OLS but lost significance once estimation was corrected.

Applying **HC3 robust standard errors** appropriately widened confidence intervals, surfacing the true inferential landscape. The correction revealed that the model's apparent explanatory precision was partly an artifact of error misspecification, not genuine signal strength. Coefficients on high-collinearity deployment features were particularly affected.

> **Takeaway:** In high-variance CapEx regimes — such as the AI infrastructure scaling environment represented in this dataset — uncorrected OLS is not merely inefficient; it is actively misleading. Robust estimation is not a refinement; it is a prerequisite for credible inference.

---

## Tech Stack

| Tool | Role |
|---|---|
| Python | Core analysis environment |
| pandas | Data ingestion and feature engineering |
| statsmodels | OLS estimation, diagnostic tests, HC3 robust errors |
| matplotlib / seaborn | Residual diagnostics and inference visualization |

---
