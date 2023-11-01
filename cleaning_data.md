What issues will you address by cleaning the data?





Queries:
Below, provide the SQL queries you used to clean your data.


-- ALL SESSIONS

-- First, I will see what's within the table.

SELECT * FROM all_sessions;


-- I'll check if there are duplicates

WITH cte AS 

(	<br>
  SELECT visitid, COUNT(id) as visits<br>
	FROM all_sessions<br>
	GROUP BY 1<br>
	ORDER BY 2 DESC<br>
)

SELECT *<br>
FROM all_sessions<br>
JOIN cte USING (visitid)<br>
WHERE visits > 1<br>
ORDER BY 1;<br>


-- I will divide the column 'productprice' by 1,000,000 and convert it into a REAL type.<br>
-- This will be added into a new column.

ALTER TABLE all_sessions<br>
ADD productpricedivided REAL;	
	
UPDATE all_sessions<br>
SET	productpricedivided = CAST(productprice AS REAL)/1000000;

SELECT * FROM all_sessions;


-- Check which columns have only NULLS and delete them.

SELECT 	DISTINCT (ecommerceaction_option)<br>
FROM	all_sessions;

--Using SELECT DISTINCT I checked the different values for each column finding the following 4 columns to be completely empty:

/*productrefundamount<br>
itemquantity<br>
itemrevenue<br>
searchkeyword*/

ALTER TABLE all_sessions<br>
DROP COLUMN productrefundamount;

ALTER TABLE all_sessions<br>
DROP COLUMN itemrevenue;

ALTER TABLE all_sessions<br>
DROP COLUMN itemquantity;

ALTER TABLE all_sessions<br>
DROP COLUMN searchkeyword;

-- Which column should I use to measure revenue?


SELECT * FROM all_sessions;

SELECT * FROM all_sessions WHERE totaltransactionrevenue > 0;

-- 'totaltransactionrevenue' seems to be the most populated column about revenue.



-- ANALYTICS

SELECT * FROM analytics;


-- visitid & visitstarttime are the same? I will check

SELECT visitid, visitstarttime,<br>
		CASE 	WHEN visitid = visitstarttime THEN 1 ELSE 0 END<br>
FROM analytics<br>
ORDER BY 3 ;  					

-- They're not



-- I will divide the column 'unit_price' by 1,000,000 and convert it into a REAL type.<br>
-- This will be added into a new column.


ALTER TABLE analytics<br>
ADD unitpricedivided REAL;	
	
UPDATE analytics<br>
SET	unitpricedivided = CAST(unit_price AS REAL)/1000000;



-- Checking empty columns
-- Potential: userid, units_sold, timeonsite, revenue

SELECT 	DISTINCT (userid)
FROM	analytics;

-- I repeat the previous query for all the other 3 columns

-- only 'userid' to be deleted. 

ALTER TABLE analytics<br>
DROP COLUMN userid;

-- In 'units_sold' there's an outlier with a value of -89. Revenue value is NULL. I will delete the whole row.

DELETE FROM analytics <br>
WHERE units_sold = -89;

SELECT * FROM analytics;


-- PRODUCTS

SELECT * FROM products;


-- SALES_BY_SKU

SELECT * FROM sales_by_sku;

-- SALES_REPORT

SELECT * FROM sales_report;

-- Nothing out of normal found in the other 3 tables
