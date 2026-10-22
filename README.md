

# GoExplore Sales Analytics Dashboard

##  Project Overview

The **GoExplore Sales Analytics Dashboard** is a Business Intelligence project designed to monitor sales performance and support data-driven decision-making.

The project uses **Google BigQuery** for data preparation and SQL-based analysis, and **Looker Studio** to create interactive dashboards that transform raw sales data into actionable business insights.

The dashboard helps stakeholders monitor revenue trends, compare sales performance across years, evaluate product and retailer performance, and analyze estimated profitability.

##  Project Objectives

- Monitor overall sales revenue and performance.
- Analyze monthly and yearly revenue trends.
- Measure month-over-month (MoM) and year-over-year (YoY) revenue growth.
- Compare equivalent periods across years.
- Evaluate estimated gross profit and gross margin.
- Identify high-performing products, retailers, and countries.
- Present key business insights in an accessible, interactive dashboard.

##  Tools & Technologies

| Technology | Purpose |
|---|---|
| Google BigQuery | Data storage, SQL transformations, and analytical views |
| SQL | Data preparation, joins, aggregations, and KPI calculations |
| Looker Studio | Interactive dashboards and visualizations |
| Google Cloud | Cloud-based analytics infrastructure |

##  Data Sources

The project uses four tables from the `GoExplore` dataset in BigQuery.

| Table | Description |
|---|---|
| `daily_sales` | Sales dates, retailer codes, product codes, quantities, prices, and order methods |
| `retailer` | Retailer names, types, and countries |
| `products` | Product names, categories, brands, colors, unit costs, and prices |
| `methods` | Order method codes and descriptions |

### Data Relationships

The `daily_sales` table is joined with the reference tables using the following keys:

- `daily_sales.Retailer_code` = `retailer.Retailer_code`
- `daily_sales.Product_number` = `products.Product_number`
- `daily_sales.Order_method_code` = `methods.Order_method_code`

These joins enrich sales records with retailer, product, and order method information.

##  Data Preparation

The main analytical view is:

`wbs-sabah.GoExplore.sale_view`

The view combines sales records with retailer, product, and order method attributes.

It also derives date fields from the `DATE`-typed source column:

- `sales_date` — transaction date
- `sales_year` — calendar year
- `sales_month` — month number
- `sales_month_start` — first day of the month
- `sales_year_date` — first day of the year

These fields support time-based analysis, chronological sorting, and dashboard filters.

##  Key Performance Indicators (KPIs)

| KPI | Description |
|---|---|
| Total Revenue | Total sales revenue for the selected period |
| Monthly Revenue | Revenue generated in each month |
| Month-over-Month Growth | Revenue change compared with the previous month |
| Monthly Year-over-Year Growth | Revenue change compared with the same month in the previous year |
| Yearly Revenue | Total revenue for each calendar year |
| Yearly Revenue Growth | Revenue change compared with the previous year |
| January–July Revenue | Revenue generated during the first seven months of each year |
| January–July Revenue Growth | Revenue change compared with the same seven-month period in the previous year |
| Estimated Gross Profit | Revenue minus estimated product cost |
| Estimated Gross Margin | Estimated gross profit divided by revenue |

### Metric Definitions

**Revenue**

```text
Revenue = Quantity × Unit Sale Price
```

**Estimated Gross Profit**

```text
Estimated Gross Profit = Quantity × (Unit Sale Price − Unit Cost)
```

**Estimated Gross Margin**

```text
Estimated Gross Margin = Total Estimated Gross Profit / Total Revenue
```

**Revenue Growth**

```text
Revenue Growth = (Current Period Revenue − Previous Period Revenue)
                 / Previous Period Revenue
```

Growth rates are undefined when the previous period has zero or missing revenue.

## Fair Year-over-Year Comparison

The dataset contains complete monthly data for 2015, 2016, and 2017, while 2018 contains data only from January through July.

Comparing full-year totals with the incomplete 2018 period would produce misleading conclusions.

To improve comparability, the project calculates:

- Revenue from January through July for every year.
- Revenue growth for January through July compared with the same period in the previous year.

This approach provides a consistent basis for evaluating year-over-year performance.

##  Dashboard Features

The Looker Studio dashboard is designed to support ongoing business performance monitoring.

Planned or supported analytical features include:

- Revenue KPI scorecards
- Monthly revenue trend analysis
- Yearly revenue comparison
- Revenue growth indicators
- Year selection filters
- Product performance analysis
- Country and retailer performance analysis
- Estimated gross profit and gross margin analysis

Additional filters can be introduced for product categories, retailer types, and order methods.

##  How to Use the Dashboard

1. Open the Looker Studio report.
2. Select the year you want to analyze.
3. Review the revenue and growth KPIs.
4. Explore the monthly revenue trend to identify patterns and changes.
5. Use January–July metrics for fair comparisons between years.
6. Analyze product, retailer, and country breakdowns to investigate performance drivers.

##  Data Quality and Limitations

- **Estimated profitability:** Gross profit is an estimate based on the available unit cost and sales price fields. It may not include all operating, logistics, marketing, or other business costs.
- **Join integrity:** Reference tables should have unique keys to avoid duplicating sales records during joins.
- **Incomplete periods:** Full-year comparisons involving 2018 require caution because only seven months of data are available.
- **Growth calculations:** Growth rates may be `NULL` if the previous period has no valid revenue.
- **Repeated aggregates:** Monthly and yearly aggregate fields are repeated across transaction-level rows in the main view. They should not be summed directly in Looker Studio, as this can inflate results.
- **Market share:** Actual market share cannot be calculated without external market-size data.

##  Future Improvements

- Add automated data quality checks.
- Expand profitability analysis by product and country.
- Identify best- and worst-performing products.
- Analyze revenue contribution by product category.
- Measure retailer productivity and average revenue per active retailer.
- Compare order method performance.
- Add alerts for unusual revenue changes.
- Explore sales forecasting and seasonality.

## Project Outcome

The GoExplore Sales Analytics Dashboard provides a structured foundation for monitoring sales performance through cloud-based analytics and interactive visualization.

By combining BigQuery SQL transformations with Looker Studio reporting, the project converts raw sales records into business-oriented metrics that support performance monitoring, trend analysis, and informed decision-making.

---

**Project Type:** Business Intelligence / Sales Analytics  
**Tools:** Google BigQuery · SQL · Looker Studio · Google Cloud
**Team-Work:** Mehrnoosh Mohebi Damabi, Navid Modir Khazeni(https://github.com/Navid-Modir-Khazeni)), Andreas Kunz(https://github.com/Agentic-Content)
