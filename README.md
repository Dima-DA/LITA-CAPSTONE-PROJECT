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

## Technical Considerations
- Proper handling of NULL values in SUBSCRIPTIONEND
- Use of DATEDIFF for accurate duration calculations
- Consistent use of WHERE clauses for filtering
- Proper grouping for aggregation analysis

## Business Impact
1. Customer Segmentation Insights
2. Churn Analysis Capabilities
3. Revenue Pattern Recognition
4. Geographic Performance Metrics
5. Subscription Type Effectiveness
