# Recovering Experimental Truths via Propensity Score Matching
### *Causal Inference on the Lalonde Observational Dataset*

---

## Objective

Reconstruct a credible estimate of the Average Treatment Effect from observational data by modeling and correcting for selection bias — demonstrating that rigorous matching methods can recover experimental-grade causal evidence from non-randomized samples.

---

## Methodology

- **Diagnosing Observational Failure:** Established a naive baseline by computing the raw difference in mean earnings between treated and control units. The resulting estimate of -$15,204 is not a finding — it is a symptom. It reflects the systematic difference between *who self-selects into training* and *who does not*, rather than the effect of training itself. This is the Selection Bias problem in its most visible form.

- **Propensity Score Estimation via Logistic Regression:** Modeled the conditional probability of treatment assignment as a function of pre-treatment covariates — age, education, race, marital status, degree attainment, and lagged earnings (`re74`, `re75`) — using a logistic regression classifier. The resulting propensity score collapses the multi-dimensional confounder space into a single scalar, enabling like-for-like comparisons across the treatment boundary.

- **Covariate Balancing via Nearest Neighbor Matching:** Applied 1:1 Nearest Neighbor matching with replacement to pair each treated unit with its closest analog in the control pool, as measured by propensity score distance. Matching with replacement was used deliberately to minimize bias in the presence of a sparse, asymmetric control group — a known structural feature of the Lalonde observational sample.

- **Causal Effect Estimation on the Matched Sample:** Re-estimated the treatment effect on the balanced, matched dataset using a two-sample T-test, isolating the earnings differential attributable to the training program net of selection.

---

## Key Findings

| Estimate | Value |
|---|---|
| Naive (Unadjusted) Difference | -$15,204 |
| PSM-Recovered Treatment Effect | ~+$1,800 |
| Known Experimental Benchmark | ~+$1,795 |

The matched estimator recovered a treatment effect of approximately **+$1,800** — within rounding error of the experimental ground truth established by the randomized control trial in the companion dataset. The near-perfect alignment between the PSM estimate and the benchmark validates both the matching strategy and the covariate selection. The gap between the naive estimate and the recovered effect — a swing of over **$17,000** — quantifies the magnitude of selection bias present in the raw observational data and underscores why unadjusted comparisons in non-experimental economic data are not merely imprecise, but structurally misleading.

---

*Dataset: Lalonde, R. J. (1986). Evaluating the econometric evaluations of training programs with experimental data. The American Economic Review, 76(4), 604–620.*
