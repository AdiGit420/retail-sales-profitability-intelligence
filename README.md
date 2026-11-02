# Retail Sales & Profitability Intelligence

## Project overview

An end-to-end Power BI portfolio project that explores retail sales,
profitability, customer segments, product categories, sales trends, and
returns. The project demonstrates data preparation, data-quality
assessment, data modelling, DAX measures, interactive reporting, and
business interpretation.

> **Dataset note:** This project uses a synthetic practice dataset. It
> is not real company or customer data.

## Tools

-   Microsoft Power BI Desktop
-   Power Query
-   DAX
-   Excel / CSV

## Dashboard pages

### 1. Executive Overview

Provides a high-level view of business performance through: - Total
Sales - Gross Profit - Profit Margin - Total Orders - Monthly sales
trend - Sales by product category - Gross profit by product category -
Sales channel slicer

The overview screenshot showed approximately ₹10.92M in sales, ₹2.01M in
gross profit, an 18.38% profit margin, and 1,200 orders. These are
rounded dashboard display values.

### 2. Customer Analysis

Explores: - Unique customers - Sales by customer segment - Gross profit
by customer segment - Customer-level sales and profitability - Segment
slicer

The dashboard showed Consumer as the largest segment by sales
(approximately ₹5.0M), followed by Corporate (approximately ₹3.5M) and
Small Business (approximately ₹2.3M).

The customer-level table does not include orders with missing CustomerID
values. This is intentional: those orders cannot be reliably attributed
to a named customer. The discrepancy between the table total and overall
sales is documented as an unassigned-customer data-quality limitation,
not treated as a calculation error.

### 3. Returns & Operations Analysis

Includes: - Returned Orders - Return Rate - Returned Orders by Reason -
Monthly Returns Trend

The final return measures show 64 valid returned orders and a 5.33%
return rate against 1,200 orders. Three orphan return IDs that do not
match an order in the cleaned Orders table are excluded from the valid
returned-order measure.

The reason chart shows the following counts: - Late Delivery: 20 -
Damaged: 19 - Wrong Item: 14 - Changed Mind: 11

## Data preparation and quality work

The source practice pack contains raw Orders, Customers, Products, and
Returns tables. Separate cleaned queries were created in Power Query
while retaining raw queries for traceability.

Key preparation work included: - Removing duplicate OrderIDs (12
duplicate rows) and duplicate customer records (2 records). - Applying
appropriate data types, including locale-aware date conversion. -
Standardizing inconsistent category capitalization. - Checking missing
IDs, dates, quantities, discounts, and financial values. - Checking
negative quantities and product price/cost consistency. - Identifying
return records whose OrderIDs do not exist in the cleaned Orders
table. - Recording data-quality issues and documenting treatment
decisions rather than inventing missing values.

Known issues documented during the project include: - 4 missing
OrderDate values. - 9 missing CustomerID values. - 5 missing ProductID
values. - 6 missing Quantity values. - 4 DiscountRate values of 1.25
(125%), which were flagged rather than silently changed. - 5 negative
Quantity values, which were retained and flagged for review. - 1 product
where UnitCostINR exceeds ListPriceINR. - 1 missing customer Segment. -
3 orphan return records. - 1 product category capitalization
inconsistency, standardized in the cleaned product query.

## Data model

The intended analytical relationships are: -
`Customers_Clean[CustomerID]` (one) → `Orders_Clean[CustomerID]`
(many) - `Products_Clean[ProductID]` (one) → `Orders_Clean[ProductID]`
(many) - `Orders_Clean[OrderID]` (one) → `Returns_Clean[OrderID]` (many)

Raw and QA queries are retained for auditability and should not be used
as report dimensions or connected into the core analytical model.

## Core DAX measures

The project includes measures for: - Total Sales - Total Cost - Gross
Profit - Profit Margin % - Total Orders - Units Sold - Total Customers -
Returned Orders - Return Rate %

Valid returned orders are counted by intersecting return OrderIDs with
OrderIDs in the cleaned Orders table, so orphan return IDs are not
counted.

Example:

``` dax
Returned Orders =
COUNTROWS(
    INTERSECT(
        VALUES(Returns_Clean[OrderID]),
        VALUES(Orders_Clean[OrderID])
    )
)
```

``` dax
Return Rate % =
DIVIDE([Returned Orders], [Total Orders], 0)
```

## Business observations

Based on the dashboard: 1. Office products contribute approximately
₹6.0M in sales, compared with approximately ₹4.9M from Electronics. 2.
Office products also show higher gross profit (approximately ₹1.2M) than
Electronics (approximately ₹0.8M). 3. Consumer customers are the largest
sales segment, contributing approximately ₹5.0M. 4. The valid return
rate is 5.33%, or 64 returned orders out of 1,200 orders. 5. Late
Delivery and Damaged are the two largest displayed return reasons,
together accounting for 39 of the 64 valid returned orders. 6. The
monthly return trend varies over time, with the chart showing its
highest point around October 2025.

These are descriptive findings from a synthetic dataset, not causal
conclusions or claims about a real retailer.

## Limitations and interpretation

-   The dataset is synthetic and intended for learning and portfolio
    demonstration.
-   Missing customer/product/date/quantity values limit some analyses.
-   Missing CustomerID orders are not represented in customer-level
    attribution.
-   Invalid discounts, negative quantities, pricing anomalies, and
    orphan returns are flagged for business review rather than
    automatically "fixed" without evidence.
-   Return rate is based on distinct valid returned OrderIDs divided by
    total distinct orders; it is not a unit-level return rate.

## Suggested next steps

-   Recheck relationships and measures in Power BI Desktop before
    publishing.
-   Capture clean screenshots of all three report pages.
-   Publish the PBIX and this README together in a portfolio repository.
-   Clearly label the dataset as synthetic.
