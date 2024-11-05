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
