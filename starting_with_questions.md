Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


-- BY CITY --
SELECT   city, SUM(productprice) AS transactionrevenue
FROM     allsessions al
JOIN     salesbysku sbs USING(productsku)
WHERE    productprice <> 0  
         AND city <> 'not available in demo dataset' 
         AND city <> '(not set)'          
GROUP BY country, city
ORDER BY transactionrevenue DESC;  


Answer: Mountain View, New York, San Francisco


-- BY COUNTRY --
SELECT   country, SUM(productprice) AS transactionrevenue
FROM     allsessions al
JOIN     salesbysku sbs USING(productsku)
WHERE    productprice <> 0  
         AND country <> '(not set)'  
GROUP BY country
ORDER BY transactionrevenue DESC;  


Answer: United States, United Kingdom, Canada


**Question 2: What is the average number of products ordered from visitors in each city and country?**


-- BY CITY --
WITH cte_productsbycity AS (SELECT   country, city, SUM(sbs.totalordered) AS totalproductsordered
       			    FROM     allsessions al
			    JOIN     salesbysku sbs USING(productsku)
			    WHERE    totalordered <> 0
				     AND city <> 'not available in demo dataset'
		       		     AND city <> '(not set)'
			    GROUP BY country, city)

SELECT   city, AVG(totalproductsordered) AS avgproductsordered
FROM     cte_productsbycity
GROUP BY country, city
ORDER BY city;


Answer: Adelaide (3.00), Ahmedabad (90.00), Akron (13.00)


-- BY COUNTRY --
WITH cte_productsbycountry AS (SELECT   country, SUM(sbs.totalordered) AS totalproductsordered
       			       FROM     allsessions al
			       JOIN   	salesbysku sbs USING(productsku)
			       WHERE    totalordered <> 0
					AND country <> '(not set)'
			       GROUP BY country)
							   
SELECT   country, AVG(totalproductsordered) AS avgproductsordered
FROM     cte_productsbycountry
GROUP BY country
ORDER BY country;


Answer: Albania (50.00), Algeria (9.00), Argentina (497.00)


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


-- BY CITY --
SELECT   city, productcategory, COUNT(productcategory) AS countproductcategory
FROM     allsessions al
JOIN     salesbysku sbs USING(productsku)
WHERE    city <> 'not available in demo dataset'
		 AND city <> '(not set)'
	     AND productcategory <> '(not set)'
GROUP BY country, city, productcategory
ORDER BY countproductcategory DESC


Answer: In many cities the greatest number of products have been ordered from the Apparel product category, specifically the Men's Apparel sub-category.


-- BY COUNTRY --
SELECT   country, productcategory, COUNT(productcategory) AS countproductcategory
FROM     allsessions al
JOIN     salesbysku sbs USING(productsku)
WHERE    country <> '(not set)'
	     AND productcategory <> '(not set)'
GROUP BY country, productcategory
ORDER BY countproductcategory DESC


Answer: In many countries the greatest number of products have been ordered from the Apparel or Shop by Brand product categories. 


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


-- BY CITY --
CREATE TEMP TABLE totalproductsbycity AS (SELECT   country, city, sr.productname, SUM(totalordered) AS totalorderedbycity
					  FROM     salesreport sr
					  JOIN     allsessions al USING(productsku)
					  WHERE    totalordered <> 0
       						   AND city <> 'not available in demo dataset'
	   					   AND city <> '(not set)'
					  GROUP BY country, city, sr.productname
					  ORDER BY country, city, totalorderedbycity DESC);
										  
WITH cte_topsellingproductsbycity AS (SELECT country, city, productname, RANK() OVER(PARTITION BY country, city ORDER BY totalorderedbycity DESC) AS 						      topsellingproducts
FROM   totalproductsbycity)

SELECT city, productname
FROM   cte_topsellingproductsbycity
WHERE  topsellingproducts = 1;


Answer: [Buenos Aires, Sport Bag], [Rosario, Men's Vintage Badge Tee Black], [Santa Fe,	SPF-15 Slim & Slender Lip Balm]


-- BY COUNTRY --
CREATE TEMP TABLE totalproductsbycountry AS (SELECT   country, sr.productname, SUM(totalordered) AS totalorderedbycountry
					     FROM     salesreport sr
					     JOIN     allsessions al USING(productsku)
					     WHERE    totalordered <> 0
       					     	      AND country <> '(not set)'
					     GROUP BY country, sr.productname
					     ORDER BY country, totalorderedbycountry DESC);

WITH cte_topsellingproductsbycountry AS (SELECT country, productname, RANK() OVER(PARTITION BY country ORDER BY totalorderedbycountry DESC) AS topsellingproducts
					 FROM   totalproductsbycountry)

SELECT country, productname
FROM   cte_topsellingproductsbycountry
WHERE  topsellingproducts = 1;


Answer: [Albania, 22 oz  Bottle Infuser], [Algeria, Twill Cap], [Argentina, Hard Cover Journal]


**Question 5: Can we summarize the impact of revenue generated from each city/country?**


-- BY CITY --
SELECT   city, SUM(sr.totalordered * al.productprice) AS revenuebycity
FROM     allsessions al
JOIN     salesreport sr USING(productsku)
WHERE    productprice <> 0
         AND totalordered <> 0
         AND city <> 'not available in demo dataset' 
         AND city <> '(not set)'
GROUP BY country, city
ORDER BY country, city;


Answer: [Buenos Aires, 641], [Rosario, 18], [Santa Fe, 120]


-- BY COUNTRY--
SELECT   country, SUM(sr.totalordered * al.productprice) AS revenuebycountry
FROM     allsessions al
JOIN     salesreport sr USING(productsku)
WHERE    productprice <> 0
         AND totalordered <> 0
         AND country <> '(not set)'
GROUP BY country
ORDER BY revenuebycountry DESC;


Answer: [United States, 5281227], [United Kingdom, 249795], [Canada, 164436]




