What issues will you address by cleaning the data?

Missing Values: Identifying and handling missing values in the dataset, ensuring that there are no gaps in the data that could affect analysis results. Techniques such as imputation (replacing missing values with estimated values) or deletion (removing records with missing values) can be employed to address this issue.

Duplicates: Identifying and removing duplicate records from the dataset to avoid double-counting and ensure data accuracy. Duplicate records can skew analysis results and lead to incorrect conclusions if not addressed properly.

Inconsistencies: Standardize data formats and values to ensure consistency across the dataset. Address inconsistencies such as variations in capitalization, spelling errors, or different representations of the same data (e.g., "USA" vs. "United States").

Data Integrity: Validate data integrity by checking for constraints and relationships between tables. Ensure that foreign key constraints are enforced and that data relationships are maintained to prevent data corruption or inaccuracies.

Outliers: Identifying and handling outliers in the dataset, which may skew analysis results or impact the distribution of the data. Techniques such as trimming (removing extreme values) or winsorizing (replacing extreme values with less extreme values) can be used to address outliers.

Data Quality Metrics: Calculating and analyzing data quality metrics such as completeness, accuracy, and consistency to assess the overall quality of the dataset.

Data Cleaning Queries:

Example 1: Removing columns with too many null values from All Sessions table. 
ALTER TABLE allsessions
DROP COLUMN totaltransactionrevenue,
DROP COLUMN transactions,
DROP COLUMN sessionqualitydim,
DROP COLUMN productrefundamount,
DROP COLUMN productquantity,
DROP COLUMN productrevenue,
DROP COLUMN productvariant,
DROP COLUMN itemquantity,
DROP COLUMN itemrevenue,
DROP COLUMN transactionrevenue,
DROP COLUMN transactionid,
DROP COLUMN searchkeyword,
DROP COLUMN ecommerceactionoption;

Example 2: Modifying the product price table to reflect the actual price of the products. 
UPDATE allsessions
SET productprice = productprice / 1000000;
