What are your risk areas? Identify and describe them.
1. Data Accuracy:
          - Incorrect product information such as pricing, descriptions, or attributes.
2. Data Completeness:
          - Missing or incomplete records for products, transactions, or customers.
3. Data Usability:
          - Poor data formatting that hinders analysis or reporting.

   
QA Process:
Check for NULL Values: Ensure that critical columns do not contain NULL values, preventing unexpected behavior and maintaining data integrity.

Check for Zero Values: Verify that numeric columns do not contain zero values, ensuring the validity of calculations and preventing errors.

Check for Unexpected Values: Ensure that categorical columns do not contain unexpected values, maintaining data consistency and preventing misinterpretation.

Ordering Results: Order the results appropriately to present them logically and meaningfully, aiding interpretation and analysis.

Calculating Rankings: Calculate rankings based on specific criteria to identify top performers or anomalies within the dataset.

Comprehensive Data Coverage: Ensure that Quality Assurance check queries cover all relevant aspects of the data and analysis process, verifying data integrity, correctness of calculations, and appropriateness of filters and conditions applied.


QA Query Examples:


Example 1: Which cities and countries have the highest level of transaction revenues on the site?


SELECT   *
FROM    (SELECT   city, SUM(productprice) AS transactionrevenue
         FROM     allsessions al
         JOIN     salesbysku sbs USING(productsku)
         WHERE    productprice <> 0  
         	        AND city <> 'not available in demo dataset' 
         	        AND city <> '(not set)'          
         GROUP BY country, city
         ORDER BY transactionrevenue DESC) AS subquery  
WHERE    transactionrevenue = 0  -- QA: Check for NULL values in productprice column
         OR city = 'not available in demo dataset' -- QA: Check for 'not available in demo dataset' in city column
         OR city = '(not set)'  -- QA: Check for '(not set)' in city column         
         OR city IS NULL  -- QA: Check for NULL values in city column
GROUP BY city, transactionrevenue
HAVING   COUNT(*) > 0  -- QA: Check for proper grouping
ORDER BY transactionrevenue DESC;  -- QA: Confirm proper ordering


Example 2: What is the average number of products ordered from visitors in each city and country?
SELECT   *
FROM     cte_productsbycity
WHERE    totalproductsordered = 0  -- QA: Check for NULL values in totalproductsordered column
		 OR city = 'not available in demo dataset'  -- QA: Check for 'not available in dataset' in city column
		 OR city = '(not set)'  -- QA: Check for '(not set)' in city column
GROUP BY country, city, totalproductsordered
HAVING   COUNT(*) > 0  -- QA: Check for proper grouping
ORDER BY city;


Example 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?


SELECT   *
FROM    (SELECT   country, city, productcategory, COUNT(productcategory) AS countproductcategory
         FROM     allsessions al
         JOIN     salesbysku sbs USING(productsku)
         WHERE    city <> 'not available in demo dataset'
	        AND city <> '(not set)'
	        AND productcategory <> '(not set)'
         GROUP BY country, city, productcategory
         ORDER BY countproductcategory DESC) AS subquery
WHERE    country IS NULL OR city IS NULL OR productcategory IS NULL  -- QA: Check for NULL values
         OR countproductcategory <= 0  -- QA: Check for negative count values
         OR (country = '' OR city = '' OR productcategory = '')  -- QA: Check for empty strings
ORDER BY countproductcategory DESC;




