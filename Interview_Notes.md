# Interview Notes --- Retail Sales & Profitability Intelligence

## 30-second project explanation

"I built a three-page Power BI dashboard using a synthetic retail
dataset. I used Power Query to clean and profile Orders, Customers,
Products, and Returns data, documented data-quality issues, created a
relational model, and wrote DAX measures for sales, gross profit,
margin, orders, customers, and returns. The report has an executive
overview, customer analysis, and returns analysis."

## 90-second project explanation

"The goal was to create a retail performance report that could help a
business understand revenue, profitability, customer contribution, and
returns. I started by inspecting the raw tables and creating cleaned
Power Query queries while preserving the original data. I removed
duplicate order and customer records, standardized category
capitalization, corrected data types and date interpretation, and
created QA checks for missing IDs, missing dates, invalid discounts,
negative quantities, and orphan returns.

I then modelled the cleaned customer, product, order, and return tables
and created DAX measures such as Total Sales, Gross Profit, Profit
Margin, Total Orders, Returned Orders, and Return Rate. Finally, I built
three report pages: Executive Overview, Customer Analysis, and Returns &
Operations Analysis. One important decision was not to invent missing
CustomerIDs or silently correct suspicious values. I documented those
issues because they affect how the results should be interpreted."

## Resume project entry

**Retail Sales & Profitability Intelligence \| Power BI, Power Query,
DAX, Excel** - Built a 3-page Power BI dashboard to analyze retail
sales, gross profit, customer segments, product categories, and returns
using a synthetic dataset. - Cleaned and transformed Orders, Customers,
Products, and Returns data in Power Query; removed duplicate records,
standardized categories, and documented data-quality exceptions. -
Developed DAX measures for sales, cost, gross profit, profit margin,
orders, customers, returned orders, and return rate; created a
relational data model and interactive slicers. - Identified key patterns
including category and segment sales contribution and a 5.33% valid
order return rate (64 of 1,200 orders).

## Questions you should be ready to answer

1.  Why did you keep raw tables instead of overwriting them?
    -   To preserve source data, make transformations traceable, and
        support quality checks.
2.  Why did you not fill missing CustomerIDs?
    -   There was no reliable source for the missing identities.
        Guessing would create false customer attribution.
3.  How did you handle orphan return records?
    -   I identified the three return OrderIDs that did not match a
        cleaned order and excluded them from the valid returned-order
        KPI while documenting the issue.
4.  How is Return Rate calculated?
    -   Distinct valid returned OrderIDs divided by distinct total
        OrderIDs.
5.  What is the difference between sales and gross profit?
    -   Sales is revenue; gross profit is sales less recorded cost.
6.  What would you improve with real business data?
    -   Validate the business definitions with stakeholders, investigate
        data-quality exceptions with source-system owners, add
        time-intelligence comparisons, and confirm return and margin
        definitions.

## Important honesty note

Do not describe the synthetic dataset as company data, do not claim the
dashboard was deployed to a real business, and do not claim business
impact or revenue improvement. Describe it as a self-directed portfolio
project.
