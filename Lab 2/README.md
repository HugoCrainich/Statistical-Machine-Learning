# Lab 2: The Illusion of Growth & The Composition Effect

## Objective

This project builds a Python pipeline to ingest live economic data from the Federal Reserve API (FRED) to analyze wage stagnation and correct for statistical biases in labor market reporting. The analysis investigates the "Money Illusion"—the persistent gap between nominal wage growth and real purchasing power—and uncovers how compositional changes in the workforce can create misleading signals about economic prosperity.

## Methodology

### 1. Data Acquisition via FRED API
- **API Integration**: Leveraged the `fredapi` Python library to programmatically fetch time-series data from the Federal Reserve Economic Data system
- **Primary Dataset**: Average Hourly Earnings of Production and Nonsupervisory Employees (AHETPI), 1964–present
- **Deflator**: Consumer Price Index for All Urban Consumers (CPIAUCSL) to convert nominal wages into constant dollars
- **Validation Dataset**: Employment Cost Index (ECI) for composition-adjusted wage measurement

### 2. Real Wage Calculation
```python
Real_Wage = (Nominal_Wage / CPI) × 100
```
Adjusted all nominal earnings to constant 2023 dollars to reveal true purchasing power trends over five decades.

### 3. Anomaly Detection: The 2020 Pandemic Spike
Time-series analysis revealed an unprecedented surge in real wages during Q2-Q3 2020, contradicting the economic devastation of the pandemic lockdowns.

### 4. Composition Effect Correction
- **Hypothesis**: The 2020 wage spike was a statistical artifact caused by low-wage workers disproportionately leaving the labor force
- **Validation**: Cross-referenced with the Employment Cost Index (ECI), which controls for changes in workforce composition by tracking fixed job categories
- **Result**: ECI data confirmed no true wage increase—the spike disappeared when controlling for composition bias

## Key Findings

### The Money Illusion (1964–Present)
Nominal wages have risen dramatically over 50 years, creating an illusion of prosperity. However, when adjusted for inflation, **real wages have remained essentially flat since the 1970s**. Workers today have roughly the same purchasing power as their counterparts half a century ago, despite apparent "raises."

### The Pandemic Paradox (2020 Anomaly)
The data revealed a sharp spike in real wages during 2020—seemingly paradoxical given widespread unemployment and business closures. Investigation uncovered the root cause:

**The Composition Effect**: When low-wage service workers (retail, hospitality, food service) were disproportionately laid off during lockdowns, the remaining workforce skewed toward higher-wage positions. This created the statistical illusion of a wage boom, even though no individual worker received meaningful raises.

**Evidence**: The Employment Cost Index, which tracks wages for fixed job categories and eliminates composition bias, showed **no corresponding spike**. This proved the 2020 wage increase was purely a statistical artifact—a measurement error, not an economic reality.

### Implications
This analysis demonstrates the critical importance of controlling for compositional changes when interpreting labor market statistics. Headlines celebrating "wage growth" can mask stagnation or even reflect workforce contraction rather than genuine prosperity.

---

## Tech Stack
- **Python 3.x**
- **fredapi** - Federal Reserve API client
- **pandas** - Time-series data manipulation
- **matplotlib** - Data visualization

## Visualization
The project produces a dual time-series chart comparing nominal vs. real wages, with annotation highlighting the 2020 composition effect anomaly.
