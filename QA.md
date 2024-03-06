What are your risk areas? Identify and describe them.
1. Data Accuracy:
2. Data Completeness:
3. 


QA Process:
Describe your QA process and include the SQL queries used to execute it.

Starting with Questions:

Question 1: Which cities and countries have the highest level of transaction revenues on the site?
Sub-Query Quality Assurance Check: 

Question 2: Sub-Query Quality Assurance (QA) Check

SELECT DISTINCT(city),
       country
FROM   allsessions
WHERE  city <> 'not available in demo dataset'
AND    city <> '(not set)'
AND	   productprice <> 0;
