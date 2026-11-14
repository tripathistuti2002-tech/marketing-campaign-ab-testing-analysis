# A/B Testing Analysis: Facebook vs. AdWords Marketing Campaign

An end-to-end A/B testing and campaign performance analysis in Python, comparing Facebook and AdWords ads over a full year (365 days, 2019) to guide budget and targeting decisions.

## Business Problem

A company runs ads on two platforms, Facebook and AdWords. The marketing team wants to know:

- Which platform generates more conversions?
- Is the difference statistically significant, or just chance?
- How strongly do clicks translate into conversions on each platform?
- When (day of week and month) does the best platform perform best and cost least?
- Where should the next marketing rupee/dollar go?

## Dataset

File: `marketing_campaign_data.csv` (365 daily rows, 1 Jan 2019 to 31 Dec 2019)

| Column Group | Columns |
| :--- | :--- |
| Date | `Date` |
| Facebook | `Facebook_Views`, `Facebook_Clicks`, `Facebook_Conversions`, `Facebook_Cost_per_Ad`, `Facebook_CTR`, `Facebook_Conversion_Rate`, `Facebook_Cost_per_Click`, `Facebook_Cost_per_Conversion` |
| AdWords | `AdWords_Views`, `AdWords_Clicks`, `AdWords_Conversions`, `AdWords_Cost_per_Ad`, `AdWords_CTR`, `AdWords_Conversion_Rate`, `AdWords_Cost_per_Click`, `AdWords_Cost_per_Conversion` |

## Tools and Techniques

- **Language and libraries:** Python, Pandas, NumPy, Matplotlib, Seaborn, SciPy, Scikit-learn, Statsmodels
- **Environment:** Google Colab / Jupyter Notebook
- **Techniques:** Data cleaning, EDA, distribution analysis, correlation analysis, two-sample hypothesis testing (Welch's t-test), simple linear regression, time-series and seasonality analysis, cointegration test

## Project Workflow

1. **Data loading and checks:** Shape, data types, duplicates, missing values, date conversion
2. **Distribution analysis:** Histograms of daily clicks and conversions for both platforms
3. **Conversion categories:** Days grouped into bands (`< 6`, `6–10`, `10–15`, `> 15`) and compared side by side
4. **Clicks vs. conversions:** Scatter plots and correlation coefficients
5. **Hypothesis test:** Welch's t-test ($H_0$: Facebook mean conversions $\le$ AdWords mean conversions)
6. **Regression:** Facebook clicks to conversions, with $R^2$, MSE, and sample predictions
7. **Seasonality:** Weekly and monthly conversions and monthly cost per conversion for Facebook
8. **Cointegration test:** Long-run relationship between Facebook ad cost and conversions

## Key Findings

| Metric | Facebook | AdWords |
| :--- | :--- | :--- |
| Mean daily clicks | 43.65 | 40.82 |
| Mean daily conversions | 11.63 | 4.99 |
| Median daily conversions | 12 | 5 |
| Max daily conversions | 21 | 10 |
| Clicks vs. conversions correlation | 0.88 | 0.45 |

- **Facebook converts about 2.3x more than AdWords.** The t-test gives $t = 33.91$ and $p = 1.90 \times 10^{-140}$, so the null hypothesis is rejected.
- **Click volume is similar, conversion is not.** Both platforms get roughly 41 to 44 clicks a day, so the gap comes from what happens after the click.
- **AdWords is stuck at the low end.** It had fewer than 6 conversions on 226 of 365 days (62%) and never exceeded 10 in a day.
- **Facebook is more predictable.** The regression explains 76.81% of the variation in conversions ($\text{MSE} = 2.41$), predicting about 12.56 conversions at 50 clicks and 16.95 at 80 clicks.
- **Best days:** Monday and Tuesday (weakest: Saturday, Friday, and Sunday).
- **Best months:** September to December have the highest volume. May, November, and December have the lowest cost per conversion (about 7.1 to 7.4), while February and March are the most expensive (about 8.1 to 8.4).
- **Spend alone is not enough.** The cointegration test ($\text{score} = -2.46$, $p = 0.2969$) found no evidence of a stable long-run link between Facebook spend and conversions.

## Business Recommendations

- **Shift budget toward Facebook**, which delivers more than double the conversions from similar click volume.
- **Concentrate spend on Mondays and Tuesdays**, and review creatives or reduce bids on the weakest days.
- **Scale up in September to December**, and in May, when cost per conversion is also low.
- **Audit February and March**, where cost per conversion is highest, for targeting and bidding problems.
- **Improve quality, not just spend:** test new creatives, audiences, and bidding strategies.
- **Fix AdWords before dropping it:** clicks are healthy but few convert, which points to landing page or targeting issues.
- **Increase Facebook budget gradually** and track cost per conversion at each step.

## Limitations

- Cost per conversion was analysed only for Facebook, so the platforms are not yet compared on cost efficiency.
- The two channels ran over the same period and were not randomly assigned, so results show association rather than proven cause.
- The regression was evaluated on the same data it was trained on, with no train/test split.
- A non-significant cointegration result means no evidence of a relationship, not proof that none exists.
