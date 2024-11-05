# LITA-CAPSTONE-PROJECT
# Data Analysis Project Portfolio

## Project Overview
This project focuses on analyzing customer subscription patterns and sales performance using two primary datasets.

## Datasets Description

### 1. Customer Subscription Dataset
This dataset contains information about customer subscriptions and their characteristics:
- SubscriptionType (Is the Primary focus with three types)
- Revenue
- Suscription dates
- Canelled subscriptions

**Primary Use**: Understanding customer subscription patterns and preferences

### 2. Sales Dataset
This comprehensive sales dataset includes the following columns:
- OrderID (Unique identifier for each order)
- Customer ID (Links to customer data)
- Product (Product information)
- Region (Geographical sales region)
- OrderDate (Timestamp of orders)
- Quantity (Units ordered)
- UnitPrice (Price per unit)
- SALES (Total sales value)

**Primary Use**: Analyzing sales performance, regional trends, and customer purchasing behavior

## Analysis Goals
This project aims to:
1. Analyze subscription patterns and customer preferences
2. Identify sales trends across different regions
3. Study the relationship between subscription types and purchasing behavior
4. Generate insights for business decision-making

## Tools and Technologies Used
- [Excel, SQL, Power BI ]

# Customer Subscription Data Analysis

## Data Overview and Excel Methodology

### 1. Subscription Type Revenue Analysis
#### Key Findings:
- Total Revenue: $149,819,686.00
- Revenue Distribution:
  - Basic: $74,756,784.00 (49.9%)
  - Premium: $37,580,782.00 (25.1%)
  - Standard: $37,482,120.00 (25.0%)

#### Excel Techniques Used:
- PivotTable creation for revenue aggregation
- Pie chart visualization with percentage distribution
- Custom formatting for currency values

### 2. Canceled Subscription Analysis
#### Key Findings:
- Cancellation Patterns:
  * Basic Subscriptions:
    - Active (FALSE): $52,340,173.00
    - Canceled (TRUE): $22,416,611.00
  * Premium Subscriptions:
    - Active (FALSE): $15,051,884.00
    - Canceled (TRUE): $22,528,898.00
  * Standard Subscriptions:
    - Active (FALSE): $14,954,166.00
    - Canceled (TRUE): $22,528,898.00

#### Excel Techniques Used:
- Nested PivotTable with Subscription Type and Cancellation Status
- Column chart visualization
- Boolean filtering (TRUE/FALSE for cancellation status)
- Custom data labels

### 3. Regional Revenue Distribution
#### Key Findings:
- Even distribution across regions:
  * East: $37,387,894.00
  * North: $37,368,890.00
  * South: $37,580,782.00
  * West: $37,482,120.00

#### Excel Techniques Used:
- PivotTable with region and subscription type
- Line and column combination chart
- Power trendline addition
- Custom axis formatting

## Key Insights

1. **Subscription Distribution:**
   - Basic subscriptions generate the highest revenue, indicating a strong base-tier customer preference
   - Premium and Standard tiers contribute equally to revenue

2. **Cancellation Patterns:**
   - Higher cancellation rates in Premium and Standard subscriptions
   - Basic subscriptions show better retention with lower cancellation rates

3. **Regional Performance:**
   - Remarkably consistent revenue across all regions
   - Indicates successful market penetration and balanced regional strategy

## Excel Methodology Used
1. Data Cleaning and Preparation:
   - Removed duplicates
   - Verified data consistency

2. Analysis Tools:
   - PivotTables for data aggregation
   - Custom calculations
   - Advanced filtering

3. Visualization Techniques:
   - Pie charts for distribution analysis
   - Column charts for comparison
   - Combination charts for trend analysis

<img width="354" alt="Excel CUSTOMER DATA" src="https://github.com/user-attachments/assets/c36c2206-125a-4f55-b90d-1255b762ce70">

# SQL Analysis Documentation: Customer Data

## 1. Data Importation and Exploration
```sql
-- Converted Excel file to csv and imported into SQL
-- Initial data exploration
SELECT * FROM [dbo].[ProjectCustomerData]
```
**Purpose**: Initial examination of all customer data fields and records

## 2. Regional Customer Distribution
```sql
SELECT REGION, COUNT(CustomerID) AS CUSTOMER_BY_REGION 
FROM [dbo].[ProjectCustomerData] 
GROUP BY REGION
```
**Purpose**: Analyze customer distribution across regions
**Key Insight**: Shows regional market penetration and customer concentration

## 3. Most Popular Subscription Type
```sql
SELECT TOP(1) SUBSCRIPTIONTYPE, COUNT(CustomerID) AS TOP_SUB_TYPE  
FROM [dbo].[ProjectCustomerData] 
GROUP BY SUBSCRIPTIONTYPE
```
**Purpose**: Identify the most preferred subscription plan
**Business Value**: Helps in understanding customer preferences and pricing strategy effectiveness

## 4. Early Subscription Cancellations
```sql
SELECT COUNT(CustomerID) AS CANCELED_SUB  
FROM [dbo].[ProjectCustomerData] 
WHERE CANCELED = 0 
AND DATEDIFF(MONTH, SUBSCRIPTIONSTART, SUBSCRIPTIONEND) <= 6
```
**Purpose**: Identify early churn rate (cancellations within 6 months)
**Risk Analysis**: Helps identify potential issues with customer satisfaction or onboarding

## 5. Average Subscription Duration
```sql
SELECT AVG(DATEDIFF(MONTH, SUBSCRIPTIONSTART, 
    CASE 
        WHEN SUBSCRIPTIONEND IS NULL THEN GETDATE()
        ELSE SUBSCRIPTIONEND
    END)) AS ASVSUB
FROM [dbo].[ProjectCustomerData]
```
**Purpose**: Calculate average customer lifetime
**Technical Note**: Uses CASE statement to handle active subscriptions

## 6. Long-Term Customer Analysis
```sql
SELECT CUSTOMERID, CUSTOMERNAME, SUBSCRIPTIONTYPE 
FROM [dbo].[ProjectCustomerData]
WHERE DATEDIFF(MONTH, SUBSCRIPTIONSTART, 
    CASE 
        WHEN SUBSCRIPTIONEND IS NULL THEN GETDATE()
        ELSE SUBSCRIPTIONEND
    END) > 12
```
**Purpose**: Identify loyal customers (>12 months subscription)
**Business Value**: Helps in understanding characteristics of long-term customers

## 7. Revenue Analysis by Subscription
```sql
SELECT SUM(REVENUE) AS REV_BY_SUBTYPE 
FROM [dbo].[ProjectCustomerData]
GROUP BY SUBSCRIPTIONTYPE
```
**Purpose**: Analyze revenue contribution by subscription type
**Financial Impact**: Helps in revenue forecasting and pricing strategy

## 8. Top Cancellation Regions
```sql
SELECT TOP(3) REGION, COUNT(*) AS CANCELED_COUNT
FROM [dbo].[ProjectCustomerData]
WHERE CANCELED = 1
GROUP BY REGION
ORDER BY CANCELED_COUNT DESC
```
**Purpose**: Identify regions with highest churn rates
**Strategic Value**: Helps in targeting retention efforts geographically

## 9. Subscription Status Overview
```sql
SELECT 
    CASE
        WHEN CANCELED = 1 THEN 'NONACTIVE'
        ELSE 'ACTIVE'
    END AS SUBSCRIPTIONCOUNT,
    COUNT(*) AS SUBSTATUS
FROM [dbo].[ProjectCustomerData]
GROUP BY CANCELED
```
**Purpose**: Overall active vs. canceled subscription analysis
**Business Metrics**: Key performance indicator for customer retention

## Key SQL Techniques Used
1. Aggregation Functions (COUNT, SUM, AVG)
2. CASE Statements for conditional logic
3. DATEDIFF for time-based calculations
4. GROUP BY for data aggregation
5. TOP clause for limiting results
6. NULL handling with CASE statements
7. Date manipulation functions



## Power BI Dashboard Overview
The "LITA CUSTOMER SALES DASHBOARD" presents a comprehensive view of customer subscription data with multiple interactive visualizations and key metrics.

## Key Components Analysis

### 1. Revenue Distribution by Region (Pie Chart)
- Total Revenue: ~150M
- Even distribution across regions:
  * South: 38M (25.07%)
  * West: 37M (24.94%)
  * East: 37M (24.90%)
  * North: 37M (25.09%)

### 2. Top Performing Subscription Types (Bar Chart)
Revenue by subscription tier:
- Basic: 75M (highest performer)
- Premium: 38M
- Standard: 37M

### 3. Key Metrics Cards
- Total Number of Subscribers: 75K
- Subscription Status:
  * Active (FALSE): 41,250 subscribers
  * Canceled (TRUE): 33,750 subscribers
- Total Revenue: 150M

### 4. Average Revenue by Year (Table)
Quarterly breakdown for 2023-2024:
```
2023:
- Q1: 2002.27
- Q2: 2000.28
- Q3: 1991.92
- Q4: 1996.91

2024:
- Q1: 1985.36
- Q2: 2005.11
- Q3: 2003.20
```

### 5. Revenue by Subscription Type and Region (Stacked Bar Chart)
- Shows distribution of subscription types across regions
- 100% stacked visualization for proportional comparison
- Clear segmentation between Basic, Premium, and Standard subscriptions

## Interactive Elements
1. Region Filter:
   - East
   - North
   - South
   - West

2. Subscription Type Filter:
   - Basic
   - Premium
   - Standard

## Dashboard Design Elements
1. Color Coding:
   - Consistent color scheme for regions
   - Distinct colors for subscription types
   - Highlighted metrics in separate cards

2. Layout:
   - Clean grid arrangement
   - Clear visual hierarchy
   - Effective use of white space

## Key Business Insights
1. Customer Base:
   - 75,000 total subscribers
   - 55% retention rate (41,250 active vs 33,750 canceled)

2. Revenue Performance:
   - 150M total revenue
   - Basic subscription is the strongest performer
   - Even regional distribution suggests successful market penetration

3. Subscription Patterns:
   - Basic type dominates revenue generation
   - Premium and Standard types show similar performance
   - Consistent regional distribution across subscription types

## Visualizations Used:
   - Pie chart for regional distribution
   - Bar charts for subscription performance
   - Stacked bar chart for detailed breakdown
   - Cards for key metrics
   - Table for time series data

   
<img width="474" alt="Customer Data Power BI" src="https://github.com/user-attachments/assets/136d36be-ee4f-48ad-9bc0-88c3bbe58976">

## Sales Data Analysis- Excel

### 1. Data Exploration
- Examined the data structure and columns: Product, Sum of SALES, Sales by Quarter, and Region by Sales
- Verified the completeness and accuracy of the data

### 2. Sales by Product Analysis
- Created a bar chart to visualize the sales by product
- Key insights:
  - Shoes is the highest selling product, generating over 3M in sales
  - Gloves and Hat are the next best-selling products, contributing around 2M each
  - Shirt, Socks, and Jacket have lower sales in comparison

### 3. Sales by Quarter Analysis
- Constructed a line chart to analyze the quarterly sales trends
- Key insights:
  - Sales have been relatively stable over the past 6 quarters, ranging from 65K to 90K
  - Q1 and Q3 tend to have the highest sales, while Q2 and Q4 have slightly lower sales
  - This suggests potential seasonality in the sales patterns

### 4. Sales by Region Analysis
- Utilized a pie chart to understand the regional sales distribution
- Key insights:
  - Sales are evenly distributed across the four regions (East, North, South, West)
  - Each region contributes around 25% of the total sales
  - This indicates a balanced regional sales strategy and successful market penetration
 
    <img width="285" alt="Sales data excel" src="https://github.com/user-attachments/assets/c9d9a04a-1f3f-40d1-9a6a-26a82df25cad">
## Sales Data Analysis- SQL

### 1. Total Sales by Region
```sql
SELECT
    Region,
    SUM(SALES_REVENUE) AS TOTAL_SALES_REGION
FROM [dbo].[SALESDATA-LITA-PROJECT]
GROUP BY Region
```
**Key Insights:**
- The sales are fairly evenly distributed across the four regions (East, North, South, West).

### 2. Highest Selling Product
```sql
SELECT
    Product,
    SUM(SALES_REVENUE) AS TOTAL_SALES_PRODUCT
FROM [dbo].[SALESDATA-LITA-PROJECT]
GROUP BY Product
ORDER BY TOTAL_SALES_PRODUCT DESC
```
**Key Insights:**
- Shoes is the highest selling product, contributing the most to the overall sales revenue.
- Gloves and Hat are the next top-performing products.
- Understanding the drivers behind the success of these best-selling products can inform product development and inventory management.

### 3. Total Revenue per Product
```sql
SELECT
    Product,
    SUM(SALES_REVENUE) AS TOTAL_SALES_PRODUCT
FROM [dbo].[SALESDATA-LITA-PROJECT]
GROUP BY Product
```
**Key Insights:**
- This query provides a breakdown of the total revenue generated by each product.
- The results can be used to identify the most and least profitable products, enabling targeted strategies for product optimization.

### 4. Monthly Sales Total for 2024
```sql
SELECT
    MONTH(ORDERDATE) AS MONTH,
    SUM(SALES_REVENUE) AS TOTAL_SALES_MONTHLY
FROM [dbo].[SALESDATA-LITA-PROJECT]
WHERE ORDERDATE BETWEEN '2024-01-01' AND '2024-12-31'
GROUP BY MONTH(ORDERDATE)
ORDER BY MONTH(ORDERDATE)
```
**Key Insights:**
- This analysis provides a monthly breakdown of sales revenue for the year 2024.
- The results can be used to identify any seasonal trends or fluctuations in sales, which can inform production planning, inventory management, and marketing strategies.

### 5. Top 5 Customers by Total Purchase
```sql
SELECT TOP 5
    CUSTOMER_ID,
    SUM(SALES_REVENUE) AS HIGH_BUYING_CUSTOMERS
FROM [dbo].[SALESDATA-LITA-PROJECT]
GROUP BY CUSTOMER_ID
ORDER BY SUM(SALES_REVENUE) DESC
```
**Key Insights:**
- This query identifies the top 5 customers with the highest total purchase value.
- Targeting these high-value customers with personalized offers, loyalty programs, or exclusive products can help drive further sales and revenue growth.

### 6. Percentage of Total Sales Contributed by Each Region
```sql
SELECT
    Region,
    SUM(SALES_REVENUE) AS REGION_CONTRIBUTION,
    (SUM(SALES_REVENUE) * 100.0 / (SELECT SUM(SALES_REVENUE) FROM [dbo].[SALESDATA-LITA-PROJECT])) AS PERCENTAGE_CONTRIBUTION
FROM [dbo].[SALESDATA-LITA-PROJECT]
GROUP BY Region
ORDER BY PERCENTAGE_CONTRIBUTION DESC
```
**Key Insights:**
- This analysis provides the percentage contribution of each region to the overall sales revenue.
- The results show a well-balanced distribution, with each region contributing around 25% of the total sales.
- This indicates a successful regional sales strategy and market coverage.

### 7. Products with No Sales
```sql
SELECT Product
FROM [dbo].[SALESDATA-LITA-PROJECT]
WHERE SALES_REVENUE = 0
```
**Key Insights:**
- This query identifies any products that have not generated any sales revenue.
- Analyzing the reasons behind the lack of sales for these products can help inform product optimization, discontinuation, or targeted marketing strategies.

  ## Sales Data Analysis- Power BI

### 1. Overall Sales Performance
- Total Sales: $11M
- Total Quantity Sold: 345,000 units

### 2. Sales by Region
- The sales are evenly distributed across the four regions (East, North, South, West), with each region contributing around 2M in sales.

### 3. Top Performing Subscription Types
- Basic subscriptions generate the highest revenue at $75M, followed by Premium at $38M and Standard at $37M.

### 4. Average Revenue by Year
- The average quarterly revenue has remained relatively stable over the past 2 years, ranging from $1.99M to $2.01M.

### 5. Subscription Status
- There are 41,250 active (FALSE) subscriptions and 33,750 canceled (TRUE) subscriptions.

### 6. Sales by Product and Quarter
- Shoes are the highest selling product, contributing the most to the overall sales.
- Sales trends show a seasonal pattern, with Q1 and Q3 typically being the strongest quarters.

### 7. Sales by Subscription Type and Region
- The regional distribution of subscription types is relatively balanced, with each region having a similar mix of Basic, Premium, and Standard subscriptions.


<img width="611" alt="sales data Power bi" src="https://github.com/user-attachments/assets/5a927ae7-1de3-448a-ae3a-ec749a2b8497">

## Summary of the Data Set

The comprehensive analysis of the customer subscription and sales data provides a detailed understanding of LITA's business performance and customer dynamics.

### Key Takeaways:

1. **Customer Base and Retention**:
   - The company has a substantial customer base of 75,000 subscribers.
   - However, the churn rate is relatively high, with 41,250 active subscribers and 33,750 canceled subscriptions.
   - Identifying and addressing the factors leading to early subscription cancellations (within 6 months) could help improve customer retention.

2. **Subscription Type Performance**:
   - Basic subscriptions generate the highest revenue, accounting for 75M out of the 150M total revenue.
   - Premium and Standard tiers contribute equally at around 37-38M in revenue each.
   - Understanding the drivers behind the popularity of Basic subscriptions can inform pricing and packaging strategies.

3. **Regional Analysis**:
   - Revenue is consistently distributed across the four regions (East, North, South, West), suggesting successful market penetration.
   - The regional distribution of subscription types is also balanced, indicating a cohesive go-to-market strategy.
   - Monitoring any regional shifts in performance or customer preferences can help refine targeted sales and marketing efforts.

4. **Revenue Trends**:
   - The average quarterly revenue has remained relatively stable over the past 2 years, ranging from 1.99M to 2.01M.
   - Identifying any seasonal or cyclical patterns in revenue can assist with financial forecasting and planning.

5. **Long-Term Customer Value**:
   - The analysis of customers with subscriptions longer than 12 months provides insights into LITA's loyal user base.
   - Understanding the characteristics and behaviors of these long-term customers can inform strategies to acquire and retain similar high-value subscribers.

Overall, the data-driven insights from this analysis can empower LITA to make informed decisions, optimize its subscription offerings, enhance customer retention, and drive sustainable business growth.
