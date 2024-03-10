Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**
-- BY CITY --
SELECT   city, SUM(productprice) AS transactionrevenue
FROM     allsessions al
JOIN     salesbysku sbs USING(productsku)
WHERE    productprice <> 0 -- QA: Remove NULL values from productprice column
         AND city <> 'not available in demo dataset' -- QA: Remove 'not available in demo dataset' values from city column
         AND city <> '(not set)' -- QA: Remove '(not set)' values from city column         
	 AND city IS NOT NULL  -- QA: Check for NULL values in city column
GROUP BY country, city
HAVING   COUNT(*) > 0  -- QA: Check for proper grouping
ORDER BY transactionrevenue DESC;  -- QA: Confirm proper ordering


-- BY COUNTRY --
SELECT   country, SUM(productprice) AS transactionrevenue
FROM     allsessions al
JOIN     salesbysku sbs USING(productsku)
WHERE    productprice <> 0 -- QA: Remove NULL values from productprice column
         AND country <> '(not set)' -- QA: Remove '(not set)' values from country column
         AND country IS NOT NULL  -- QA: Check for NULL values in country column
GROUP BY country
HAVING   COUNT(*) > 0  -- QA: Check for proper grouping
ORDER BY transactionrevenue DESC;  -- QA: Confirm proper ordering

Answer: Mountain View, New York, San Francisco

**Question 2: What is the average number of products ordered from visitors in each city and country?**

SQL Queries:
WITH cte_productsorderedbycustomer AS (SELECT   COUNT(fullvisitorid) AS productsordered,
						fullvisitorid,
						city,
						country
       				       FROM     allsessions
				       WHERE	city <> 'not available in demo dataset'
		       		       AND 	city <> '(not set)'
				       AND	productprice <> 0
				       GROUP BY fullvisitorid,
						city,
						country)
										       
SELECT   AVG(productsordered) AS avgproductsordered,
         city,
	 country
FROM     cte_productsorderedbycustomer
GROUP BY city,
         country;

Answer:

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**

SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







