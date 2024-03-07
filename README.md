# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
(fill in your description and goals here)

## Process
STEP 1: EXPLORE CVS FILES.
- Identify columns, their names, data types
- Look for duplicate values, irrelevant observations, null values
- Identify PRIMARY KEY and FOREIGN KEY (if applicable)

STEP 2: TABLE CREATION IN POSTGRESQL. CODE USED BELOW: 

-- CREATE ALL SESSIONS TABLE --
CREATE TABLE allsessions (
  fullvisitorid VARCHAR (50),
  channelgrouping VARCHAR (20),
  visittime BIGINT,
  country VARCHAR (20),
  city VARCHAR (30),
  totaltransactionrevenue BIGINT,
  transactions SMALLINT,
  timeonsite SMALLINT,
  pageviews SMALLINT,
  sessionqualitydim SMALLINT,
  visitdate DATE,
  visitid CHAR (10),
  visittype VARCHAR (5),
  productrefundamount SMALLINT,
  productquantity SMALLINT,
  productprice BIGINT,
  productrevenue BIGINT,
  productsku VARCHAR (20),
  productname VARCHAR (100),
  productcategory VARCHAR (100),
  productvariant VARCHAR (20),
  currencycode CHAR (3),
  itemquantity SMALLINT,
  itemrevenue BIGINT,
  transactionrevenue BIGINT,
  transactionid VARCHAR (20),
  pagetitle VARCHAR,
  searchkeyword VARCHAR (50),
  pagepathlevel1 VARCHAR (50),
  eCommerceActiontype SMALLINT,	
  eCommerceActionstep SMALLINT,
  eCommerceActionoption VARCHAR (50)
);

-- CREATE ANALYTICS TABLE --
CREATE TABLE analytics (
  visitnumber SMALLINT,
  visitid CHAR (10),
  visitstarttime CHAR(10),
  visitdate DATE,
  fullvisitorid VARCHAR (50),
  userid VARCHAR (50),
  channelgrouping VARCHAR (20),
  socialengagementtype VARCHAR (30),
  unitssold SMALLINT,
  pageviews SMALLINT,
  timeonsite SMALLINT,
  bounces SMALLINT,
  revenue BIGINT,
  unitprice BIGINT
);

-- CREATE PRODUCTS TABLE --
CREATE TABLE products (
  productsku VARCHAR (20),
  productname VARCHAR (100),
  orderedquantity SMALLINT,
  stocklevel SMALLINT,
  restockingleadtime SMALLINT,
  sentimentscore NUMERIC,
  sentimentmagnitude NUMERIC, 
  PRIMARY KEY (productsku)
);

-- CREATE SALES BY SKU --
CREATE TABLE salesbysku (
  productsku VARCHAR(20),
  totalordered SMALLINT,
  PRIMARY KEY (productsku)
);

-- CREATE SALES REPORT --
CREATE TABLE salesreport (
  productsku VARCHAR (20),
  totalordered SMALLINT,
  productname VARCHAR (100),
  stocklevel SMALLINT,
  restockingleadtime SMALLINT,
  sentimentscore NUMERIC,
  sentimentmagnitude NUMERIC,
  ratio NUMERIC,
  PRIMARY KEY (productsku)
);

STEP 3: IMPORT DATA INTO POSTGRESQL FROM CSV FILES.
STEP 4: DATA CLEANING. CODE BELOW:




### (your step 2)

## Results
(fill in what you discovered this data could tell you and how you used the data to answer those questions)

## Challenges 
(discuss challenges you faced in the project)

## Future Goals
(what would you do if you had more time?)
