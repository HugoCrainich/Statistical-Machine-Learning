# Hypothesis Testing & Causal Evidence Architecture
### *The Epistemology of Falsification: Hypothesis Testing on the Lalonde Dataset*

---

## Objective

Most applied analytics workflows are optimized for **estimation** — producing a number, a coefficient, a predicted value. This project deliberately pivots from that paradigm toward **falsification**: the practice of structuring analysis around what the data can *disprove*, not merely what it can describe.

Using the canonical Lalonde (1986) dataset — a seminal benchmark in causal inference derived from the National Supported Work (NSW) job training program — this project operationalizes the scientific method to adjudicate between competing narratives of causality. The central question is not *"What is the effect of job training?"* but rather *"Is there sufficient statistical evidence to reject the claim that job training has no effect?"* This reframing transforms an estimation exercise into a rigorous act of evidentiary reasoning.

---

## Technical Approach

- **Parametric Testing via Welch's T-Test (SciPy):** Computed the Average Treatment Effect (ATE) on real post-program earnings by framing it as a Signal-to-Noise problem. Welch's formulation was selected over Student's T-Test to relax the equal-variance assumption between the treatment and control groups — a common and consequential violation in observational economic data. The resulting test statistic quantifies how many standard errors separate the group means, providing a calibrated measure of evidential strength.

- **Non-Parametric Validation via Permutation Test (SciPy, 10,000 resamples):** To stress-test parametric assumptions against the non-normal, right-skewed distributions characteristic of earnings data, a permutation test was conducted using 10,000 random resamples of group labels. This distribution-agnostic approach constructs an empirical null distribution from the data itself, validating that the observed treatment effect is not an artifact of Gaussian assumptions.

- **Type I Error Control:** Both testing procedures were evaluated against a pre-specified significance threshold (α = 0.05), enforcing a disciplined boundary on the false positive rate. The alignment of p-values across both the parametric and non-parametric frameworks substantively strengthens the inferential claim — convergent evidence across methodologically independent tests is a meaningful guard against spurious findings.

---

## Key Findings

The analysis identified a statistically significant lift in real earnings of approximately **$1,795** for program participants, with the Null Hypothesis rejected under both testing regimes. The consistency of this result across a parametric and a resampling-based framework provides robust, multi-method causal evidence that the NSW job training intervention produced a measurable economic effect.

---

## Business Insight: Hypothesis Testing as the Safety Valve of the Algorithmic Economy

In production data science environments, the velocity of modeling is a liability as much as it is an asset. Modern ML pipelines can surface seemingly compelling correlations at industrial scale — and without a rigorous falsification layer, those correlations become the basis for product decisions, resource allocation, and automated interventions. This is how **data grubbing** enters the enterprise: not through malice, but through the structural pressure to ship insights fast.

Hypothesis testing is the **safety valve** in this system. It is the mechanism by which a team institutionalizes skepticism — building *disconfirmation* directly into the analytical workflow before a finding ever reaches a stakeholder deck or a model deployment checklist. By requiring that effects clear a defined evidential threshold (rather than simply appearing in a feature importance chart or a lift curve), organizations protect themselves from the compounding cost of acting on noise.

The Lalonde analysis demonstrates this architecture in miniature: a claimed causal effect is not accepted because a coefficient is positive, but because two independent statistical frameworks — one parametric, one empirical — converge on the same conclusion at a controlled false-positive rate. That convergence is the evidentiary standard. In a world where algorithmic decisions carry real economic and social consequences, that standard is not academic overhead. It is the baseline of responsible inference.

---

---

## Industry Note: Decision Thresholds as Business Parameters

Netflix's Return-Aware Experimentation framework reframes A/B testing away from scientific hypothesis validation and toward maximizing long-run returns on business metrics. Rather than treating p < 0.05 as a fixed gate, Netflix empirically evaluates candidate decision rules — including p-value thresholds themselves — by measuring their cumulative impact across hundreds of past experiments. The key insight is that while scientists are rightly driven to prevent false discoveries from entering the scientific record, businesses may be more tolerant of false positives as long as more true discoveries are unearthed — meaning the right α is a function of implementation cost and expected lift, not statistical convention. This project applies that same logic in miniature: the α = 0.05 threshold used here is a deliberate risk parameter, not an inherited rule, and the dual-method validation (parametric + permutation) reflects the kind of convergent evidence a production experimentation team would demand before committing engineering resources to a launch.

---

*Dataset: Lalonde, R. J. (1986). Evaluating the econometric evaluations of training programs with experimental data. The American Economic Review, 76(4), 604–620.*
*Netflix Return-Aware Experimentation: Ejdemyr, S. & Chou, W. et al. (2025). Evaluating Decision Rules Across Many Weak Experiments. KDD '25 Best Paper (Applied Data Science).*
