Question 1: Based on sentimentscore, how does Canada rank when compared with other countries?


WITH cte_sentimentscorebycountry AS (SELECT   'country' AS labeltype, country, AVG(sentimentscore) AS avgsentimentscore
								     FROM     allsessions al
								     JOIN     salesreport sr USING(productsku)
									 WHERE    country <> '(not set)'
								     GROUP BY country
								     ORDER BY avgsentimentscore DESC)

SELECT country, avgsentimentscore, RANK() OVER(PARTITION BY labeltype ORDER BY avgsentimentscore DESC) 
FROM   cte_sentimentscorebycountry
ORDER BY country;


Answer: Canada ranks 62 out of 126.


Question 2: Do people who buy products with a higher price generally spend a greater amount of time on the website before purchasing?


SELECT   sr.productname, productprice, AVG(timeonsite) AS avgtimeonsite
FROM     allsessions al
JOIN     salesreport sr USING(productname)
WHERE    timeonsite IS NOT NULL
	     AND productprice <> 0					
GROUP BY sr.productname, productprice
ORDER BY avgtimeonsite DESC;


Answer: There does not appear to be a relationship between amount spent on site and price of product purchased. 


Question 3: In which countries has paid advertising been most successful in generating revenue? 


SELECT   country, SUM(totalordered * productprice) AS revenue
FROM     allsessions al
JOIN     salesreport sr USING(productsku)
WHERE    channelgrouping = 'Paid Search'
GROUP BY country
ORDER BY revenue DESC;


Answer: United States, Canada, Malaysia. 


Question 4: Which months saw the most revenue generated and what factors might contribute to this pattern?


SELECT   EXTRACT(MONTH FROM visitdate) AS monthofsale, SUM(totalordered * productprice) AS revenue 
FROM     allsessions
JOIN     salesreport sr USING(productsku)
GROUP BY EXTRACT(MONTH FROM visitdate)
ORDER BY EXTRACT(MONTH FROM visitdate);


Answer: December, January, November. It makes sense that most revenue has been generated during these months since big holidays such as Christmas, New Year's, and Boxing Day fall during these months. 
