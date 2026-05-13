# Walmart Revenue Forecasting Using Retail-Sales Indicators

## Question

Can monthly retail-sales data from FRED serve as a useful leading indicator for Walmart quarterly revenue, and does 
it improve forecasting performance relative to a simple seasonal-naive baseline?

## Short Answer

Yes — retail-sales growth appears to add predictive value.
Using lagged retail-sales indicators improved out-of-sample forecasting performance relative to a seasonal-naive baseline. 
The regression model reduced RMSE from 0.120 to 0.074, an improvement of roughly 39%.
The signal is not strong enough to stand alone, but it appears directionally useful as a supplemental forecasting input.

## My Work

I combined:

* monthly retail-sales data from FRED, and
* Walmart quarterly revenue data from SEC filings.

Because both series are highly seasonal, I converted the data into year-over-year growth rates rather than using raw values directly.

1. Built a seasonal-naive baseline forecast using the same quarter from the previous year.
2. Built a regression model using lagged retail-sales growth indicators.
3. Evaluated both approaches using walk-forward out-of-sample validation to avoid look-ahead bias.

The goal was to simulate how the model would behave in a realistic forecasting setting rather than simply fitting historical data.


## Findings

The retail-sales signal consistently outperformed the naive baseline on RMSE and MAE.
This suggests that broader retail spending trends contain useful information about future Walmart revenue growth.
The relationship also appears economically intuitive:
     stronger consumer retail activity tends to align with stronger Walmart revenue growth,
     although the effect is not perfectly stable across all periods.

## Hardpoints

### 1. Structural Breaks

The relationship weakens during unusual macroeconomic periods, especially around COVID-19. Consumer behavior changed 
significantly during this period, making historical relationships less reliable.

### 2. Small Sample Size

Quarterly revenue data produces a fairly limited number of observations. That limits statistical confidence and increases 
sensitivity to unusual periods.

### 3. Timing / Data Availability

Revenue is reported after quarter-end, while retail-sales data is released on a different schedule. In production 
forecasting, timing assumptions would need to be handled carefully to avoid leakage.

### 4. Correlation Is Not Causation

Retail-sales growth may correlate with Walmart revenue without directly causing it. Both may simply react to broader 
economic conditions.

### 5. Metric Instability

MAPE became unstable because year-over-year growth can occasionally approach zero or become negative. RMSE and MAE were 
therefore more reliable measures for this analysis.


Retail-sales data appears to provide meaningful incremental forecasting value relative to a seasonal-naive benchmark, 
particularly during stable economic periods.

I would view it as a useful supporting indicator rather than a standalone forecasting signal.
