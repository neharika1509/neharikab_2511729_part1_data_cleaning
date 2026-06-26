# neharikab_2511729_part1_data_cleaning

## 1. Problem Summary
This project involves cleaning, validating, and summarizing a raw retail orders dataset. The raw data contained multiple data quality issues like missing values, duplicate records, inconsistent text formatting, mixed date formats, invalid discount values, and sales/profit calculation mismatches. The goal was to produce a fully cleaned dataset, a data quality report, and pivot summary reports that can be used for business analysis.


## 2. Dataset Description

Property - Details
File - data/raw_orders.xlsx
Total Records - 932 rows
Total Columns - 21 columns
Time Period - 2024 – 2025

Columns in the Dataset

order_id - Unique order identifier
order_date - Date the order was placed
ship_date - Date the order was shipped
customer_id - Unique customer identifier
customer_name - Name of the customer
segment - Customer segment (Consumer, Corporate, Small Business)
region - Geographic region (North, South, East, West)
state - State of the customer
city - City of the customer
category - Product category (Technology, Furniture, Office Supplies)
sub_category - Product sub-category
product_name - Name of the product
ship_mode - Shipping method used
quantity - Number of units ordered 
unit_price - Price per unit
discount - Discount applied (0 to 1)
sales - Original sales value
cost - Cost of the order
profit - Original profit value
payment_status - Payment status (Paid, Pending, Refunded, Failed)
order_status - Order status (Completed, Returned, Cancelled)


Order Status Breakdown

Status Count:
Completed - 622
Returned - 164
Cancelled - 146

Payment Status Breakdown

Status Count:
Paid - 704
Pending - 87
Refunded - 72
Failed - 69



## 3. Tools Used


Microsoft Excel — data cleaning, calculated columns, pivot tables
GitHub — version control and repository management



## 4. Cleaning Steps Performed

Task 1 — Preserve Raw Data

Kept raw_orders.xlsx completely unchanged
Created a copy named cleaned_orders.xlsx for all cleaning work


Task 2 — Clean Text Fields

Applied TRIM() and PROPER() to remove extra spaces and fix capitalization inconsistencies in: customer_name, segment, region, state, city, category, sub_category, ship_mode, payment_status, order_status
Used Find & Replace to fix similar category names written differently (e.g. "Office  Supplies" → "Office Supplies")


Task 3 — Clean and Validate Dates

Standardized order_date and ship_date from 3 mixed formats to a consistent DD/MM/YYYY format using Text to Columns
Added shipping_delay_days column = ship_date - order_date
Flagged rows where ship_date is earlier than order_date as INVALID


Task 4 — Handle Duplicates

Identified and removed 20 exact duplicate rows using Data → Remove Duplicates
Identified 32 duplicate order_id rows with conflicting information and flagged them for review (not deleted)


Task 5 — Apply Business Rules

Filled missing region values (25 rows) with "Unknown"
Filled missing ship_mode values (21 rows) with "Unknown"
Filled missing discount values (18 rows) with 0 where all other sales fields were valid
Flagged negative discounts (16 rows) as INVALID
Excluded Cancelled and Failed payment orders from completed sales summary
Summarized Refunded orders separately in pivot report




## 5. Business Rules Applied

 Rule Area - Action Taken 

 Missing region - Filled with Unknown 
 Missing ship_mode - Filled with Unknown 
 Missing discount - Treated as 0 if all other sales fields valid 
 Negative discount - Flagged as INVALID 
 Discount above 100% - Flagged as INVALID (none found) 
 Cancelled orders - Excluded from completed sales summary 
 Failed payments - Excluded from completed sales summary 
 Refunded orders - Summarized separately in pivot report 
 Ship date before order date - Flagged as invalid shipping record 



## 6. Summary of Data Quality Issues Found

 Issue - Column - Count 
 Missing region - region - 26 
 Missing ship_mode - ship_mode - 22 
 Missing discount - discount - 18 
 Negative discounts - discount - 16 
 Exact duplicate rows - all columns - 20 
 Duplicate order_ids with conflicts - order_id - 32 
 Mixed date formats - order_date, ship_date - Multiple 
 Sales calculation mismatches - sales - 62 
 Profit calculation mismatches - profit - 41 

Full details are documented in outputs/data_quality_report.xlsx.


## 7. Summary of Final Pivot Reports

All pivot tables are saved in outputs/pivot_summary.xlsx across 6 sheets:

 Sheet - Description 
 By_Region - Total sales and profit by region, sorted by sales descending 
 By_Category - Total sales and profit by category and sub-category 
 By_ShipMode - Order count by shipping mode, filtered to exclude Unknown 
 By_Segment - Profit margin by customer segment 
 Problem_Orders - Count of returned, cancelled, and failed orders by region 
 Monthly_Trend - Monthly sales trend by year and month 



## 8. Key Business Insights

- 622 out of 932 orders (67%) were successfully completed
- 164 orders were returned and 146 were cancelled, representing significant revenue loss
- 62 sales records and 41 profit records had calculation mismatches with the original values, suggesting possible data entry errors
- 16 orders had negative discounts, which are invalid and were flagged for review
- The dataset covers 4 regions (North, South, East, West) with relatively even distribution
- Technology was the largest product category with 323 orders, followed by Furniture (313) and Office Supplies (296)

---

## 9. Assumptions and Limitations

### Assumptions
- Discount values are expected to be between 0 and 1 (representing 0% to 100%)
- calculated_sales = quantity x unit_price x (1 - discount)
- calculated_profit = calculated_sales - cost
- Records with missing region or ship_mode are valid orders with incomplete data
- Duplicate order_ids with conflicting data require human review and were not deleted

### Limitations
- Some ambiguous dates may have been interpreted incorrectly since the format could be read in multiple ways
- The root cause of the 62 sales and 41 profit mismatches is unknown — original data source should be verified
- Missing region values were filled with Unknown since no external reference was available to determine correct regions
- Duplicate order_ids with conflicting information were flagged but not resolved — human review is needed



## 10. Screenshots

Screenshots of the data before and after cleaning are saved in the screenshots/ folder:

 File - Description 

 raw_data_preview.png - Preview of the original raw dataset 
 cleaned_data_preview.png - Preview of the cleaned dataset 
 pivot_summary_1.png - Screenshot of pivot tables 1 and 2 
 pivot_summary_2.png - Screenshot of pivot tables 3 through 6 



## Repository Structure

part1_data_cleaning/
├── data/
│   ├── raw_orders.xlsx
│   └── cleaned_orders.xlsx
├── outputs/
│   ├── data_quality_report.xlsx
│   ├── pivot_summary.xlsx
│   └── cleaning_log.md
├── screenshots/
│   ├── raw_data_preview.png
│   ├── cleaned_data_preview.png
│   ├── pivot_summary_1.png
│   └── pivot_summary_2.png
└── README.md
