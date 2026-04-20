## Causal ML — Double Machine Learning for 401(k) Policy Evaluation
Objective: Apply Double Machine Learning to estimate the causal effect of 401(k) eligibility on household net financial assets, isolating the treatment effect from selection bias using flexible nonparametric nuisance learners.
Methodology:

Demonstrated regularization bias by showing that naive LASSO shrinks the treatment coefficient on simulated data with a known ATE of 5.0, recovering only 4.94
Constructed a DoubleML Partially Linear Regression (PLR) model with Random Forest nuisance learners and 5-fold cross-fitting on 9,915 observations from the Chernozhukov & Hansen 401(k) dataset
Estimated the population-level Average Treatment Effect of 401(k) eligibility on net total financial assets
Conducted subgroup CATE analysis by splitting observations into income quartiles and fitting separate DML models on each

Key Findings: The overall ATE of 401(k) eligibility on net financial assets was −$867 (95% CI: −$1,810 to $76, p = 0.07), suggesting no statistically significant effect once selection bias is controlled for. CATE analysis revealed heterogeneity across income groups: the lowest-income households (Q1) showed a small positive effect of +$384, while middle and upper quartiles showed negative point estimates (Q2: −$1,546, Q3: −$865, Q4: −$1,658), though all confidence intervals crossed zero. These results suggest that 401(k) eligibility alone is insufficient to increase financial assets, and that program design matters more than eligibility status.
