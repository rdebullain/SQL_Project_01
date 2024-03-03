Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
SELECT   SUM(productprice) AS totalproductprice,
		 country,
		 city
FROM     allsessions
WHERE	 city <> 'not available in demo dataset' 
		 AND city <> '(not set)'
GROUP BY country,
		 city
ORDER BY totalproductprice DESC;



Answer: Top Ten

1. Mountain View, United States
2. New York, United States
3. San Francisco, United States
4. Sunnyvale, United States
5. San Jose, United States
6. Los Angeles, United States
7. Chicago, United States
8. Palo Alto, United States
9. London, United Kingdom
10. Seattle, United States

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:



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







