# Audit 02: Deconstructing Statistical Lies

> **Mission**: Expose how companies manipulate statistics to hide failures, exaggerate accuracy, and cherry-pick success stories.

## 📊 Executive Summary

This audit investigates three common statistical deceptions used in tech marketing:
1. **Latency Skew** - How "mean latency" hides catastrophic performance for real users
2. **False Positive Paradox** - Why 98% accuracy doesn't mean what you think it means
3. **Survivorship Bias** - The crypto market illusion created by ignoring 99% of failures

---

## 🚨 Finding #1: The Latency Trap

### The Pitch
**NebulaCloud** claims: *"Mean Latency: 35ms - Lightning fast performance!"*

### The Reality
Simulated 1,000 API requests with a realistic distribution:
- **980 requests** (98%): Normal traffic, 20-50ms
- **20 requests** (2%): Spike traffic, 1000-5000ms (app crashes, cold starts, timeouts)

### Results

| Metric | Value | What It Means |
|--------|-------|---------------|
| **Mean Latency** | 90.8ms | Looks acceptable |
| **Median Latency** | 35ms | Most users experience this |
| **95th Percentile** | 1,048ms | 1 in 20 users wait >1 second |
| **99th Percentile** | 3,942ms | 1 in 100 users wait ~4 seconds |

### The Deception
NebulaCloud's marketing focuses on the **mean**, which sounds great. But:
- **20,000 users per day** experience 1-5 second delays (if you serve 1M requests)
- Those users complain, churn, and leave bad reviews
- The "mean" is a **vanity metric** that hides operational failures

### Robust Statistics Reveal the Truth

```
Standard Deviation (SD): 419.63ms  ← Exploded by outliers
Median Absolute Deviation (MAD): 8.0ms  ← Stable, not fooled
```

**Why SD fails**: Squaring deviations amplifies outliers exponentially. A 3000ms spike contributes **2,800x more** to variance than a normal 35ms request.

**Why MAD works**: Uses medians instead of means, so extreme values can't dominate. Shows the *typical* variation, not the chaos.

---

## 🎯 Finding #2: The False Positive Paradox

### The Pitch
**IntegrityAI** plagiarism detector claims: *"98% Accurate (Sensitivity=98%, Specificity=98%)"*

### The Reality
Accuracy means nothing without considering the **base rate** of cheating.

### Bayesian Audit Results

| Scenario | Base Rate | P(Cheater \| Flagged) | Interpretation |
|----------|-----------|----------------------|----------------|
| **Bootcamp** | 50% | **98.0%** | High base rate → detector works well |
| **Econ Class** | 5% | **72.1%** | 28% of flagged students are innocent |
| **Honors Seminar** | 0.1% | **4.7%** | **95% of flagged students are innocent!** |

### The Paradox Explained

In an Honors Seminar with 10,000 students:
- **10 actual cheaters** → 10 flagged (98% sensitivity catches them)
- **9,990 honest students** → 200 flagged (2% false positive rate)
- **Total flagged: 210 students**
- **Actual cheaters: 10 (only 4.7%)**

### The Deception
IntegrityAI advertises "98% accuracy" but **never mentions base rates**. In low-cheating environments, their tool flags 20x more innocent students than guilty ones, destroying reputations and wasting investigation resources.

**Key Lesson**: Any diagnostic test (medical screening, fraud detection, plagiarism) is only as good as its base rate context.

---

## 💰 Finding #3: Survivorship Bias in Crypto

### The Pitch
Crypto influencers: *"I turned $1,000 into $100,000 by investing in tokens!"*

### The Reality
Simulated 10,000 token launches with a realistic **Pareto (Power Law) distribution**:

### Results

| Dataset | Count | Mean Market Cap | Median Market Cap |
|---------|-------|----------------|-------------------|
| **All Tokens (Reality)** | 10,000 | $2,740.84 | $1,571.78 |
| **Survivors (Top 1%)** | 100 | $44,633.52 | $32,873.03 |
| **Bias Multiplier** | — | **16.3x higher** | **20.9x higher** |

### The Graveyard Statistics
- **91.3%** of tokens never reached $5,000 market cap (essentially worthless)
- **Bottom 90%** maxed out at $4,513 or less
- **Top 1%** captured most of the market cap

### The Deception
You only hear about the **100 survivors** (Bitcoin, Ethereum, Solana). The **9,900 dead tokens** don't get mentioned on Twitter, YouTube, or CoinMarketCap.

**What this means:**
- When someone shows their "portfolio gains," they're cherry-picking winners
- The market looks 16x better when you ignore 99% of failures
- "Past performance" is meaningless when you only count survivors

---

## 🛠️ Methodology

### Tools Used
- **Python**: NumPy, Pandas, Matplotlib, Seaborn
- **Statistical Tests**: Chi-Square Goodness of Fit, Bayesian Inference
- **Distributions**: Pareto (Power Law), Uniform Random

### Key Techniques
1. **Data Generating Process (DGP)**: Manually simulated realistic distributions
2. **Robust Statistics**: MAD vs. SD to detect outlier sensitivity
3. **Bayesian Reasoning**: Prior probabilities + Bayes' Theorem for true accuracy
4. **Sample Ratio Mismatch (SRM)**: Chi-Square test to validate A/B test integrity

---

## 🎓 Key Takeaways

### For Data Scientists
- **Never trust the mean** for skewed distributions → Use percentiles (p50, p95, p99)
- **Always check base rates** before evaluating test accuracy
- **Question what's missing** from datasets → The graveyard matters more than survivors

### For Consumers
- Ask: *"What aren't they showing me?"*
- Demand: *"What's the 99th percentile?"* not just the mean
- Investigate: *"How many failures are you hiding?"*

### Red Flags in Marketing
- ✅ Claims of "mean" or "average" performance without percentiles
- ✅ Accuracy percentages without base rate context
- ✅ Success stories without failure statistics
- ✅ A/B tests with suspicious sample imbalances (SRM)

---

## 📈 Bonus: The A/B Test SRM Check

**FinFlash A/B Test**:
- Expected: 50,000 control / 50,000 treatment
- Observed: 50,250 control / 49,750 treatment
- Chi-Square: **2.5** (p > 0.05)

**Verdict**: Technically valid, but suspicious. The 500-user imbalance suggests possible crashes or data collection issues in the treatment group. **Best practice**: Investigate before trusting results.

---

## 🔗 Resources

### Code Repository
All simulations, functions, and visualizations available in this notebook.

### Further Reading
- **Taleb, N.** - *The Black Swan* (on tail risk and Pareto distributions)
- **Kahneman, D.** - *Thinking, Fast and Slow* (on base rate neglect)
- **Pearl, J.** - *The Book of Why* (on causal inference and Bayes)

---

## ⚠️ Disclaimer

These analyses are educational demonstrations. All company names (NebulaCloud, IntegrityAI, FinFlash) are fictional. Real-world applications require domain expertise, regulatory compliance, and ethical considerations.

**Remember**: Statistics don't lie, but people use them to deceive. Always audit the metrics that matter.
