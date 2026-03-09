## Structural Forensics: Diagnosing Spurious Correlation in Macroeconomic Time-Series

Investigated the risks of multicollinearity and spurious correlation in macroeconomic modeling using live data pulled from the Federal Reserve Economic Data (FRED) API. Working with five macro indicators — CPI, Unemployment, Fed Funds Rate, Industrial Production, and M2 Money Supply — across a 14-year horizon, the project demonstrates how raw level data can produce misleading statistical signals and compromise model integrity.

**Methodology:**
- Fetched and preprocessed monthly FRED data using `pandas_datareader`, normalizing series to a consistent frequency
- Visualized the correlation trap in raw levels using `seaborn` heatmaps, exposing near-perfect correlations driven by shared trends rather than structural relationships
- Quantified predictor redundancy using Variance Inflation Factor (VIF) diagnostics via `statsmodels`, identifying severe multicollinearity across trending variables
- Resolved non-stationarity by transforming variables into Year-over-Year (YoY) growth rates, significantly reducing spurious correlations
- Applied Directed Acyclic Graphs (DAGs) to encode causal assumptions, distinguishing direct causal paths from fork structures driven by unobserved confounders such as expansionary macro policy

**Tools:** Python, pandas, seaborn, statsmodels, plotly, networkx
