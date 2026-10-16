# Retail Sales & Customer Analytics Dashboard

A portfolio project using **SQL and Microsoft Excel** to analyze retail
sales, profitability, products, cities, customers, and payment patterns.

> **Data note:** This project uses a synthetic portfolio dataset.
> Metrics describe this dataset only and are not results from a real
> company.

## Table of Contents

-   [Overview](#overview)
-   [Business Questions](#business-questions)
-   [Dataset](#dataset)
-   [Tools](#tools)
-   [KPIs](#key-performance-indicators)
-   [Analysis](#analysis)
-   [Key Findings](#key-findings)
-   [Dashboard](#dashboard)
-   [Workflow](#workflow)
-   [Suggested Repository Structure](#suggested-repository-structure)
-   [How to Use](#how-to-use)
-   [Limitations](#limitations)
-   [Future Improvements](#future-improvements)
-   [Author](#author)

## Overview

Retail teams need to understand what drives sales and profit, how
performance varies by product and location, and how customer and payment
patterns change over time. This project examines **10,000 orders from
2024--2025** using SQL for analysis and Excel for dashboard reporting.

### Objectives

-   Measure sales, profit, order volume, and units sold.
-   Compare product, category, and city performance.
-   Explore monthly sales trends.
-   Review customer-type and payment-method patterns.
-   Examine discounts alongside profitability.
-   Present findings in an accessible dashboard.

## Business Questions

1.  What are total net sales and profit?
2.  How many orders, customers, and units are represented?
3.  Which categories and products contribute most to sales and profit?
4.  How does performance vary across cities?
5.  How do sales change month by month?
6.  What patterns appear by customer type and payment method?
7.  How are discounts associated with profitability?
8.  What is the average order value?

## Dataset

**File:** `Retail_Sales_Customer_Analytics.csv`

-   **Rows:** 10,000
-   **Columns:** 14
-   **Date range:** 1 January 2024 -- 31 December 2025
-   **Unique order IDs:** 10,000
-   **Unique customer IDs:** 2,449

### Data Dictionary

  Column             Description
  ------------------ ---------------------------------------------------
  `Order_ID`         Order identifier
  `Order_Date`       Order date
  `Customer_ID`      Customer identifier
  `City`             City associated with the order
  `Category`         Product category
  `Product`          Product name
  `Quantity`         Units sold
  `Unit_Price`       Unit selling price
  `Discount_Pct`     Discount percentage
  `Net_Sales`        Sales after discount
  `Cost`             Cost associated with the sale
  `Profit`           Recorded profit
  `Payment_Method`   Payment method
  `Customer_Type`    Customer classification, such as new or returning

## Tools

-   **SQL:** querying, aggregation, grouping, ranking, and comparisons.
-   **Microsoft Excel:** KPI calculations, PivotTables/charts, dashboard
    layout, and filters.
-   **CSV:** source data format.

## Key Performance Indicators

  KPI                            Result
  --------------------- ---------------
  Total Net Sales         ₹4,736,995.31
  Total Profit            ₹1,330,362.56
  Total Orders                   10,000
  Unique Customers                2,449
  Total Quantity Sold      40,267 units
  Average Order Value           ₹473.70
  Average Discount                 6.4%
  Profit Margin                   28.1%

### Metric Definitions

-   **Total Net Sales:** Sum of `Net_Sales`.
-   **Total Profit:** Sum of `Profit`.
-   **Average Order Value:** Total net sales divided by total orders.
-   **Profit Margin:** Total profit divided by total net sales,
    multiplied by 100.
-   **Average Discount:** Mean of `Discount_Pct`, expressed as a
    percentage.

These are descriptive, dataset-level metrics---not evidence of real
company performance or causal business impact.

## Analysis

### Sales and Profitability

-   Calculated total sales, profit, average order value, and profit
    margin.
-   Compared sales volume with profitability.

### Product and Category Performance

-   Compared categories and products by sales and profit.
-   Considered profit alongside revenue to avoid relying on sales value
    alone.

### Geographic Performance

-   Compared sales and profit across cities to explore location-level
    differences.

### Monthly Trends

-   Examined sales across the 2024--2025 period using date-based
    summaries.

### Customer and Payment Analysis

-   Compared performance by customer type and payment method.
-   Reviewed customer counts and sales patterns.

### Discount and Profitability

-   Examined discount levels alongside profit and margin. Any
    association should be treated as correlation, not proof of
    causation.

## Key Findings

The verified aggregate results show: - **₹47.37 lakh** in net sales and
**₹13.30 lakh** in profit. - **10,000 orders** from **2,449 unique
customers**. - **40,267 units sold**. - Average order value of
approximately **₹473.70**. - Overall profit margin of approximately
**28.1%**.

Category-, city-, product-, customer-, and payment-level views can help
identify areas for further investigation. Name a specific top-performing
category or city only when its ranking is confirmed in your SQL results
or workbook.

## Dashboard

The Excel dashboard is intended to include: - KPI cards for sales,
profit, orders, customers, and quantity. - Monthly sales trends. -
Category and product comparisons. - City-level performance. -
Payment-method and customer-type breakdowns. - Filters for year,
category, city, and customer type, where available in the workbook.

Add a screenshot to your repository and update the path below to match
the file you upload:

``` markdown
```

## Workflow

1.  Reviewed the dataset structure, fields, dates, and business
    dimensions.
2.  Validated identifiers, data types, and metric fields before
    analysis.
3.  Used SQL queries and aggregations to calculate KPIs and compare
    dimensions.
4.  Built an Excel dashboard to present the key metrics and breakdowns.
5.  Interpreted the dataset-level results and identified questions for
    further investigation.

## Limitations

-   The dataset is synthetic and does not represent a real retailer.
-   Descriptive patterns do not prove causation.
-   No real-world savings, revenue growth, or operational improvements
    are claimed.
-   Repository paths and dashboard features should be checked against
    the files actually published.

## Future Improvements

-   Publish commented, reusable SQL scripts.
-   Document data-quality checks and validation results.
-   Add month-over-month and year-over-year comparisons.
-   Add repeat-purchase or cohort analysis if supported by the data.
-   Include a final dashboard screenshot and short walkthrough.

## Author

**Shambhu Mahato**

-   LinkedIn: [Shambhu
    Mahato](https://www.linkedin.com/in/shambhu-mahato-939268240/)
-   GitHub: [Shambhu-mahato](https://github.com/Shambhu-mahato)

*Independent analytics portfolio project using synthetic data.*

