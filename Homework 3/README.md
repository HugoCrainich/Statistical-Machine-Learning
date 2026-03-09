# SwiftCart Statistical Audit
### Causal Inference & Non-Parametric Analysis Pipeline

---

## Overview

This project is a statistical audit of operational and marketing claims made by SwiftCart. The core objective is to demonstrate that surface-level statistics routinely used in corporate reporting can be misleading, and that principled non-parametric and causal methods are necessary to recover honest estimates.

The pipeline covers three distinct inferential challenges: constructing valid confidence intervals on skewed, zero-inflated compensation data; hypothesis testing under violated homoscedasticity assumptions in an A/B test; and isolating a true causal treatment effect from a loyalty program dataset contaminated by selection bias.

---

## Methodology

Where classical parametric methods break down, this pipeline replaces them with assumption-free alternatives. Bootstrap resampling and permutation testing engines are written manually using native NumPy vectorization — no high-level wrappers. Causal identification is handled through Propensity Score Matching via logistic regression and nearest-neighbor pairing, with covariate balance verified through standardized mean differences visualized on a Love Plot.

---

## Key Findings

- Median driver compensation confidence intervals are asymmetric and cannot be honestly represented by a parametric interval
- The Batch Routing algorithm produces a statistically significant reduction in delivery times even under a distribution-free test
- SwiftPass subscribers spend more post-enrollment, but roughly 44% of the claimed effect is selection bias — power users self-select into the program and would have spent more regardless

---

## Dependencies

```
numpy
pandas
matplotlib
seaborn
scikit-learn
```

---

## Usage

Execute each notebook cell sequentially. The dataset `swiftcart_loyalty.csv` is required for Phase 3 and should be uploaded when prompted.
