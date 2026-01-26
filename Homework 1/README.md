# The Cost of Living Crisis: A Data-Driven Analysis

## The Problem: Why the "Average" CPI Fails Students

The Consumer Price Index (CPI) tracks inflation for the "average" American, but students face a radically different reality. While the official CPI broadly weights hundreds of goods and services, students spend primarily on tuition (which has skyrocketed), rent, and education-related expenses—costs that have grown far faster than the national average.

## Methodology: Python, APIs, and Index Theory

This project constructs a custom **Student Price Index (SPI)** using data from the Federal Reserve Economic Data (FRED) API:

**Student Spending Basket (Laspeyres Index):**
- Tuition & Fees: 80%
- Rent: 10%
- Entertainment: 9%
- Food Out: 1%

**Technical Stack:** Python, pandas, matplotlib, fredapi  
**Time Period:** January 2016 - January 2026 (normalized to base 100)

My analysis reveals a **31.5% divergence** between Student Costs and National Inflation:

- **Student SPI**: 132 (32% increase)
- **Official National CPI**: 137 (37% increase)
- **Boston Metro CPI**: 135 (35% increase)

### Critical Insights

1. **Different Inflation Realities**: Students experienced 32% cost increases driven overwhelmingly by tuition, while the official CPI (which weights education at only ~3%) rose 37% across all goods.

2. **Regional Premium**: Boston students face both higher baseline costs and faster inflation than the national average—a compound disadvantage.

3. **Post-Pandemic Surge**: The steepest divergence occurred 2020-2023, with students and urban residents bearing disproportionate inflationary pressure.

### Bottom Line

A single national CPI masks the lived experience of students. Policymakers relying on aggregate inflation data underestimate financial stress on students, leading to inadequate adjustments in financial aid and support programs.

---

**Tools**: Python | FRED API | Pandas | Matplotlib | Laspeyres Index Theory
