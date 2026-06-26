Missing Region: There are 25 missing fields. All missing regions are found and filled with "Unknown" by using find and replace. 



Missing ship\_mode: There are 21 missing fields. All missing ship\_mode fields are filled with "unknown" using find and replace. 



Missing discount: there are 18 blank fields and are filled with 0.



Negative discount: there are 15 fields with negative discount. they are flagged as invalid in the discount\_flag column.



Discount above allowed range: there are no discounts above 100%



Cancelled orders: will not be included in the final pivot table



Failed Payments: will not be included in the final pivot table



Refunded Orders: will be summarized separately



Ship date Before Order date: they are flagged as invalid in the date\_flag column.



### **TASK 9**



\# Data Cleaning Log

Dataset: raw\_orders.xlsx  

Cleaned file: cleaned\_orders.xlsx  

Total original records: 932  

Date cleaned: 2026-06-25  





\## 1. Issues Found



&#x20;**Issue - Column - Count** 



&#x20;Missing region - region - 26 

&#x20;Missing ship\_mode - ship\_mode - 22 

&#x20;Missing discount - discount - 18 

&#x20;Negative discounts - discount - 16 

&#x20;Exact duplicate rows - all columns - 20 

&#x20;Duplicate order\_ids - order\_id - 32 

&#x20;Mixed date formats - order\_date, ship\_date - Multiple 

&#x20;Sales mismatches - sales - 62 

&#x20;Profit mismatches - profit - 41 





\## 2. Cleaning Actions Performed



\- Applied TRIM and PROPER to: customer\_name, segment, region, state, city, category, sub\_category, ship\_mode, payment\_status, order\_status

\- Standardized all dates to DD/MM/YYYY format

\- Removed 20 exact duplicate rows

\- Flagged 32 duplicate order\_id rows for review





\## 3. Business Rules Applied



\- Missing region → filled with "Unknown"

\- Missing ship\_mode → filled with "Unknown"  

\- Missing discount → filled with 0 (only where quantity, unit\_price, sales were all valid)

\- Negative discount → flagged as INVALID in cleaned\_discount column

\- Cancelled orders → excluded from completed sales summary

\- Failed payments → excluded from completed sales summary

\- Refunded orders → summarized separately in pivot report

\- Ship date before order date → flagged as INVALID in shipping\_delay\_days column





\## 4. Assumptions Made



\- Discount values should be between 0 and 1 (representing 0% to 100%)

\- calculated\_sales = quantity × unit\_price × (1 - discount)

\- calculated\_profit = calculated\_sales - cost

\- Records with missing region or ship\_mode are still valid orders, just incomplete

\- Duplicate order\_ids with conflicting data were kept and flagged, not deleted





\## 5. Records Removed



\- 20 exact duplicate rows removed







\## 6. Records Flagged



\- 32 duplicate order\_id rows flagged as "DUPLICATE ORDER ID"

\- 180 rows flagged as INVALID (final)

\- 732 rows flagged as CLEAN



\---



\## 7. Limitations



\- Date standardization was done manually; some ambiguous dates (e.g. 07/08 could be July 8 or August 7) may have been interpreted incorrectly

\- Sales and profit mismatches were recalculated but root cause is unknown

\- Duplicate order\_ids with conflicting data were not resolved — human review needed

\- No external reference was available to verify correct region for missing values



