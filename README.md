\# Jumia Product Performance \& Pricing Dashboard



An end-to-end e-commerce data analysis and interactive Microsoft Excel dashboard analyzing product pricing, promotional discounts, customer ratings, and engagement metrics for Jumia listings.





\## Project Overview



Jumia and its marketplace sellers require data-driven insights into how pricing strategies, promotional discounts, and customer ratings impact overall engagement. Because direct sales volume and revenue figures are not present in the dataset, \*\*review counts are utilized as a proxy for customer engagement\*\*.



This project processes raw e-commerce product data, performs data quality audits, standardizes messy records, enriches the dataset with logical categories and performance flags, evaluates linear correlations, and builds an interactive, single-screen Microsoft Excel dashboard.



\### Core Questions Addressed



* Are larger promotional discounts associated with higher customer engagement (reviews)?
* Do highly rated products attract stronger customer interaction?
* Do current price points move together with average customer ratings?
* Which products represent top catalog performers versus underperforming promotional risks?
* What specific pricing or marketing adjustments should sellers execute?



\## Repository Structure



```

jumia-product-performance-dashboard/

├── README.md

├── data/

│   └── Excel\_jumia\_dataset.csv

├── dashboard/

│   └── jumia\_product\_dashboard.xlsx

└── images/

         ├── raw-data.png

         ├── cleaned-data.png

         ├── pivot-tables.png

         └── dashboard.png 

```





\## Data Audit Summary

* Total Raw Records: 115 rows
* Duplicate Records: 3 full duplicate rows identified and removed (reducing clean catalog count to 112 unique products).
* Price Ranges: Evaluated and converted to midpoints on row 39 for consistent numeric analysis while preserving auditable source text.
* Missing Values: 58 missing values in ratings and reviews were treated as "uncaptured data" rather than converted to zeros.





\##  Data Cleaning \& Transformation Rules

All data transformations were executed cleanly in Cleaned\_Data (tblProducts) and documented in the workbook Data\_Dictionary:

* Product Name: Standardized using =TRIM().
* Prices: Cleaned of text characters (KSh, commas) and converted to numeric currency (KSh #,##0.00). Range values were resolved using midpoints: (Min + Max) / 2.
* Discounts: Stripped of % signs, converted to decimals, and formatted as Percentage (0%).
* Reviews: Converted negative values to absolute whole numbers via =ABS().
* Ratings: Extracted numeric values by removing " out of 5" and converted to decimals.



Calculated \& Enriched Fields

* Discount Amount: Old Price - Current Price
* Price Category: 

    Low Price: KSh 493.00 (First Quartile) 

    Medium Price: KSh 493.01 – KSh 1,669.50 (First Quartile to Third Quartile) 

    High Price: $>$ KSh 1,669.50 (Third Quartile)

*  Discount Category: Low (<20%), Medium (20% - 40%), High (>40\&)
*  Rating Category:  Poor (<3.0), Average (3.0 - 4.5), Excellent (>4.5)



\## Key Findings \& Correlation Analysis

Linear relationships were evaluated across complete paired observations using Pearson correlation (=CORREL()):



Relationship Pair         Pearson Correlation(r)    Trendline Equation   R^2 Value   Strategic Interpretation

\----------------          ---------------------     -----------------    ---------   ------------------------

Discount % vs. Reviews    -0.13682                   y = -6.11x + 14.94   0.0187      Weak Negative: Heavy discounting does not drive review engagement.

Rating vs. Reviews        +0.057209                   y = 1.15x + 8.21     0.0033     Negligible: High product ratings alone do not ensure higher review volume.

Current Price vs. Rating  +0.11009              y = 0.0001x + 3.78        0.0121     Slight Positive: Premium price points maintain solid customer satisfaction levels.







\## Business Recommendations

1. Optimize Discount Bands: Products in the Medium Discount group (20%–40%) generate higher average engagement (15.26 reviews) than items in the High Discount group (>40%, averaging 11.13 reviews). 
2. Sellers should avoid slashing prices beyond 40% as it destroys margin without boosting sales volume.
3. Audit Low-Rated, High-Discount Listings: 10 products pair high discounts (>40%) with poor ratings (<3.0). Deep price cuts on low-quality products harm brand reputation; Jumia should inspect these items for quality defects or inaccurate descriptions.
4. Promote Catalog Star Performers: 6 listings achieve both Strong Engagement (greater or equal to 14 reviews) and Excellent Ratings (>4.5). Sellers should feature these items in sponsored ad campaigns to capture high conversion rates.
5. Fix Average-Rated High-Volume Listings: 6 items generate high engagement (greater or equal to 14 reviews) but possess mediocre satisfaction ratings (3.0–4.5). Sellers should inspect buyer feedback to fix minor packaging or product flaws.



\## Data Limitations \& Analytical Challenges

* \*Engagement Proxy:\* Review count is used as a proxy for customer engagement. The dataset omits direct sales units, page views, and financial revenue.
* \*Listing Age \& Visibility:\* Review totals may reflect how long a product has been active on Jumia or its placement algorithm rather than price responsiveness.
* \*Correlation vs. Direct link:\* Observed statistical correlations do not establish direct cause-and-effect relationships.







