# Lab 5: The Architecture of Bias
**Investigating Data Generating Processes and Sampling Pathologies in Machine Learning**

---

## 📋 Overview

This lab explores how **invisible biases** enter machine learning pipelines through faulty sampling mechanisms and incomplete data observation. By reverse-engineering the Data Generating Process (DGP), we demonstrate how architectural choices in data collection create systematic errors that no algorithm can fix.

---

## 🎯 Objective

Investigate three critical failure modes in statistical inference:
1. **High-Variance Sampling Error** from Simple Random Sampling (SRS)
2. **Covariate Shift** and its elimination via Stratified Sampling
3. **Sample Ratio Mismatch (SRM)** as an indicator of engineering failures in A/B tests

---

## 🛠️ Tech Stack

- **Python 3.x**
- **pandas** – Data manipulation
- **numpy** – Numerical sampling simulations
- **scipy** – Chi-Square goodness-of-fit tests (SRM forensics)
- **sklearn** – Stratified sampling (`train_test_split` with stratification)

---

## 🔬 Methodology

### 1. **Simple Random Sampling (SRS) – The Variance Problem**
- **Action:** Manually simulated repeated random draws from the Titanic dataset
- **Finding:** High variance in survival rate estimates across samples (±8-12% fluctuations)
- **Insight:** SRS treats rare classes (e.g., first-class passengers) as equally likely to be included, leading to unrepresentative samples

### 2. **Stratified Sampling – Eliminating Covariate Shift**
- **Action:** Implemented `sklearn.model_selection.train_test_split` with `stratify=y` parameter
- **Finding:** Preserved exact class proportions across train/test splits (e.g., 38.4% survival rate maintained)
- **Insight:** Stratification guarantees that the **marginal distribution P(Y)** remains constant, preventing label shift between training and deployment

### 3. **Sample Ratio Mismatch (SRM) Forensic Audit**
- **Action:** Applied Chi-Square test to detect deviations from expected A/B test group sizes
- **Example Case:** 550/450 split on 1000 users (expected 500/500) → χ² = 10.0, p = 0.0016
- **Decision Rule:** If p < 0.01 → **CRITICAL FAILURE** (likely load balancer bug, not random chance)
- **Insight:** SRM detection prevents false positives/negatives caused by corrupted randomization logic

---

## 🔑 Key Findings

| Sampling Method | Variance | Covariate Shift Risk | Use Case |
|----------------|----------|---------------------|----------|
| Simple Random  | High     | High                | Large, homogeneous datasets |
| Stratified     | Low      | **Eliminated**      | Imbalanced classes, A/B tests |
| SRM Audit      | N/A      | Detects engineering failures | Post-hoc validation |

---

## 🧠 Theoretical Deep Dive: Survivorship Bias & Ghost Data

### **Question:**  
*Why does analyzing only successful Unicorn startups (on TechCrunch) lead to Survivorship Bias, and what specific type of Ghost Data would I need to fix it using a Heckman Correction?*

### **Answer:**

#### **The Survivorship Bias Mechanism**
When you analyze only unicorns featured on TechCrunch, you're observing a **non-random sample** conditioned on success:
```
P(Features | Unicorn) ≠ P(Features | All Startups)
```

**Why this is biased:**
- You only see startups that survived multiple funding rounds, avoided bankruptcy, and achieved $1B+ valuations
- **Ghost Data** = The thousands of failed startups with similar initial characteristics who never made it to TechCrunch
- You're estimating the effect of strategies (e.g., "raise VC early") on success, but only using data where success already occurred

**Example:**  
If 90% of unicorns "pivoted their business model," you might conclude pivoting causes success. But if 90% of *failed* startups also pivoted, then pivoting is uncorrelated with success—you just can't see the failures.

---

#### **What Ghost Data Do You Need for Heckman Correction?**

The **Heckman Selection Model** (1979 Nobel Prize) corrects survivorship bias by modeling two processes:

1. **Selection Equation** (who gets observed?)  
   `P(Startup appears on TechCrunch | X) = Φ(Zγ)`  
   Where Z includes:
   - **Venture capital raised** (even failed startups may raise seed rounds)
   - **Founder pedigree** (Stanford dropout vs. unknown founder)
   - **Industry hype cycles** (AI startups in 2023 vs. 2015)
   - **Geographic location** (Silicon Valley vs. rural Kansas)

2. **Outcome Equation** (what determines success?)  
   `Valuation = Xβ + ε`  
   Where X includes actual business fundamentals

**The Critical Ghost Data You Need:**

| Data Type | What You Observe | **Ghost Data Required** |
|-----------|------------------|-------------------------|
| **Unicorns only** | 500 successful startups | ❌ Missing |
| **Selection-corrected sample** | Same 500 unicorns | ✅ **10,000 failed startups** with same Z variables (funding, founder background, industry) |

**Specifically, you need:**
- **Failed startups' characteristics** at the *same stage* where unicorns were measured (e.g., Series A metrics)
- **Censoring indicators**: Which startups died at seed/A/B rounds vs. which were acquired vs. which went public
- **Instruments (Z variables)**: Variables that affect *selection into TechCrunch* but not *valuation directly*  
  Example: Media connections, PR budget, founder's Twitter followers

---

#### **How Heckman Fixes It:**

The Heckman model estimates:
1. **λ (Inverse Mills Ratio)** = Correction factor for selection bias
2. Includes λ as an additional regressor in the outcome equation:
```
Valuation = β₀ + β₁(Pivot) + β₂(VC_Funding) + λ(Selection_Correction) + ε
```

If λ is significant → Your original analysis was biased because "being observable" (making it to TechCrunch) was correlated with success factors.

**Without ghost data**, you're solving:  
*"What makes successful startups successful?"* (circular logic)

**With ghost data**, you're solving:  
*"What distinguishes startups that became unicorns from those that didn't?"* (causal inference)

---

## 🎓 Conclusion

Bias is not a bug—it's an **architectural feature** of how we sample reality. This lab demonstrates that:
- Sampling strategies encode assumptions about the DGP
- Violations of these assumptions (SRM, survivorship bias) corrupt inference
- Ghost data (the unseen counterfactuals) is often more important than observed data

**Key Takeaway:** Before fitting models, audit the **selection process** that generated your training data. If you can't observe failures, you can't estimate the probability of success.

---

## 📚 References
- Heckman, J. J. (1979). "Sample Selection Bias as a Specification Error." *Econometrica*.
- Kohavi, R., et al. (2009). "Controlled Experiments on the Web: Survey and Practical Guide." *Data Mining and Knowledge Discovery*.

---

**Author:** [Your Name]  
**Date:** February 2026  
**Course:** Advanced Statistical Methods / ML Engineering
