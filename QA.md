What are your risk areas? Identify and describe them.
1. Data Accuracy:
          - Incorrect product information such as pricing, descriptions, or attributes.
2. Data Completeness:
          - Missing or incomplete records for products, transactions, or customers.
3. Data Usability:
          - Poor data formatting that hinders analysis or reporting.

   
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
3. Data Completeness:
4. 


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
