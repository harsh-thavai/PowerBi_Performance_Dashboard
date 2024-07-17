# Performance Dashboard

![Performance Report_page-0001](https://github.com/user-attachments/assets/e371f23c-7410-41af-ba03-1d2afe7f9d0b)

https://app.powerbi.com/groups/me/reports/56b14cd5-6032-4d25-9230-d922f7f044b3/ReportSection?redirectedFromSignup=1,1&experience=power-bi

## Overview
This Power BI dashboard provides a comprehensive view of Plant Co.'s quantity performance. It allows for year-over-year comparisons and offers insights across different countries, products, and months.

## Key Features
- Year-to-Date (YTD) performance metrics
- Comparison with Previous Year-to-Date (PYTD)
- Country-wise performance analysis
- Monthly trends in quantity changes
- Product type breakdown (Indoor, Landscape, Outdoor)
- Account profitability segmentation

## Data Sources
- Fact_Sales: Contains transaction data including sales, quantity, and costs
- Dim_Date: Date dimension table for time-based analysis

## Main Visualizations

### 1. Key Performance Indicators (KPIs)
- YTD (Year-to-Date)
- YTD vs PYTD (Previous Year-to-Date)
- PYTD
- GP% (Gross Profit Percentage)

### 2. Bottom 10 YTD vs PYTD by Country
A chart showing the worst-performing countries in terms of year-over-year change.

### 3. Quantity YTD vs PYTD | Month - Country - Product
A chart displaying monthly trends in quantity changes, with increases and decreases highlighted.

### 4. Quantity YTD & PYTD | Month
A stacked bar chart breaking down monthly performance by product type (Indoor, Landscape, Outdoor), including a line graph showing the previous year's value.

### 5. Account Profitability Segmentation
A scatter plot showing the relationship between GP% and Value YTD.

## Interactivity
- Year selection 
- Gross Profit metric selection (options: Quantity, Sales, Gross Profit)

## DAX Measures
The dashboard uses several DAX measures for calculations. Some measures include:

```dax
// Previous Year-to-Date (PYTD) Calculations
PYTD_GrossProfit = 
CALCULATE(
    [Gross Profit],
    SAMEPERIODLASTYEAR(Dim_Date[Date]),
    Dim_Date[Inpast] = TRUE
)

// Dynamic YTD and PYTD Selections
S_YTD = 
VAR selected_values = SELECTEDVALUE(Slc_Values[Values])
VAR result = SWITCH(selected_values,
    "Sales",[YTD_Sales],
    "Quantity",[YTD_Quantity],
    "Gross Profit",[YTD_GrossProfit],
    BLANK()
)
RETURN
result

// Basic Metrics
GP% = DIVIDE([Gross Profit], [Sales])
Sales = SUM(Fact_Sales[Sales_USD])
Quantity = SUM(Fact_Sales[quantity])
Gross Profit = [Sales]-[COGs]
```
