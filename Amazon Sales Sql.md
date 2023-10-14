~~~ SQL
SELECT
* 
FROM 
sales;
~~~

~~~ SQL
/* Revenue */ 
SELECT 
      CAST(SUM(amount) 
      AS SIGNED)Revenue
FROM sales
;
~~~

~~~ SQL
/* Sales Quantity */
SELECT 
      SUM(Qty)'Sales Quantity' 
FROM sales
;
~~~

~~~ SQL
/* Total Orders */
SELECT 
      COUNT('Order ID')'Total Orders'
FROM sales
;
~~~

~~~ SQL
/* Average Order Value */
SELECT 
      CAST(SUM(amount)/COUNT('Order ID') 
      AS DECIMAL (7,2))'Average Order Value' 
FROM sales
;
~~~

~~~ SQL
/* The highest product ordered by category */
SELECT 
      MAX(category)Product 
FROM sales
;
~~~

~~~ SQL
/* Top 5 products ordered(Most Popular) */
SELECT 
      MAX(category)'Most Popular Product'
FROM sales
GROUP BY category
ORDER BY category 
DESC
LIMIT 5
;
~~~

~~~ SQL
/* Total Revenue Over Different Months */ 
SELECT
      MONTHNAME(date)Month, 
      CAST(SUM(amount)
      AS SIGNED)Revenue
FROM sales
WHERE MONTHNAME(date) IS NOT NULL
GROUP BY MONTHNAME(date)
ORDER BY Revenue
DESC
;
~~~ 

~~~ SQL
/* Peak Revenue By Month */
SELECT 
      MONTHNAME(date)Month, 
      CAST(SUM(amount)
      AS SIGNED)Revenue
FROM sales
WHERE MONTHNAME(date) IS NOT NULL
GROUP BY MONTHNAME(date)
ORDER BY Revenue 
DESC
LIMIT 1
;

~~~ SQL
/* Total Revenue Over Different Days */ 
SELECT 
      DAYOFMONTH(date)Days,
      CAST(SUM(amount)
      AS SIGNED)Revenue 
FROM sales
WHERE DAYOFMONTH(date) IS NOT NULL
GROUP BY DAYOFMONTH(date)
ORDER BY DAYOFMONTH(date) 
ASC
;
~~~

~~~ SQL
/* Peak Revenue By Days */
SELECT 
	  DAYOFMONTH(date)Days,
      CAST(SUM(amount) 
      AS SIGNED)Revenue 
FROM sales
WHERE DAYOFMONTH(date) IS NOT NULL
GROUP BY DAYOFMONTH(date)
ORDER BY Revenue 
DESC
LIMIT 3
;
~~~

~~~ SQL
/* Revenue By Category */
SELECT
      category,
      CAST(SUM(amount) 
      AS DECIMAL (10,2))Revenue 
FROM sales
GROUP BY category
ORDER BY Revenue 
DESC
LIMIT 5
;
~~~

~~~ SQL
/* Percentage of Revenue by Category */
SELECT 
      category, 
      CAST(SUM(amount)
      AS DECIMAL (10,2))Revenue,
      CAST((SUM(amount)*100)/(SELECT SUM(amount) FROM sales)
      AS DECIMAL(5,3))'%By Category'
FROM sales
GROUP BY Category
ORDER BY Revenue DESC
;
~~~

~~~ SQL
/* Revenue By Size */
SELECT 
      size,
      CAST(SUM(amount)
      AS DECIMAL (10,2)) Revenue 
FROM sales
GROUP BY size
ORDER BY Revenue
DESC
;
~~~

~~~ SQL
/* Percentage of Revenue by Size */
SELECT
      size, 
      CAST(SUM(amount) 
      AS DECIMAL(10,2))Revenue,
      CAST((SUM(amount)*100)/(SELECT SUM(amount) FROM sales) 
      AS DECIMAL(5,2))'%By Size'
FROM sales
GROUP BY Size
ORDER BY Revenue 
DESC
;
~~~

~~~ SQL
/* Top Citys By Revenue */
SELECT
	  `ship-city`,
      CAST(SUM(amount) AS SIGNED)Revenue 
      FROM sales
GROUP BY `ship-city`
ORDER BY Revenue 
DESC
LIMIT 5
;
~~~

~~~ SQL
/* Percentage of Revenue By City */
SELECT 
      `ship-city`,
      CAST(SUM(amount)
      AS SIGNED)Revenue,
      CAST((SUM(amount)*100)/(SELECT SUM(amount) FROM sales)
      AS DECIMAL(5,2))'%By Ship-city'
FROM sales
GROUP BY `ship-city`
ORDER BY Revenue
DESC
LIMIT 10
;
~~~

~~~ SQL
/* Top States By Order */
SELECT
      `ship-state`,
      COUNT(`Order ID`)`Count Order ID` 
FROM sales
GROUP BY `ship-state`
ORDER BY `Count Order ID`
DESC
LIMIT 10
;
~~~

~~~ SQL
/* Percentage Order of Contribution By State */
SELECT 
      `ship-state`, 
      COUNT('Order ID')`Count Order ID`,
      CAST((COUNT('Order ID')*100)/(SELECT COUNT('Order ID') FROM sales) 
      AS DECIMAL(4,2))'%Order Contribution'
FROM sales
GROUP BY `ship-state`
ORDER BY `Count Order ID` 
DESC
LIMIT 10 
;
~~~

~~~ SQL
/* Top States By Revenue */
SELECT
      `ship-state`,
      CAST(SUM(amount) AS SIGNED)Revenue FROM sales
GROUP BY `ship-state`
ORDER BY Revenue
DESC
LIMIT 10
;
~~~

~~~ SQL
/* Percentage of Revenue By State */
SELECT 
      `ship-state`,
      CAST(SUM(amount)
      AS SIGNED)Revenue,
      CAST((SUM(amount)*100)/(SELECT SUM(amount) FROM sales)
      AS DECIMAL(5,2))'%By Ship-state'
FROM sales
GROUP BY `ship-state`
ORDER BY Revenue
DESC
LIMIT 10
;
~~~

~~~ SQL
/* Shows the Cancelled Ordered */
SELECT
      * 
FROM sales 
WHERE  `Status`= 'Cancelled'
;
~~~

~~~ SQL
/* Trends in Order Cancellation */
SELECT 
      `Status`,
      COUNT(`Status`= 'Cancelled')`Cancelled-Order` 
FROM sales
GROUP BY `Status`
ORDER BY `Cancelled-Order`
DESC
;
~~~

~~~ SQL
/* To Check B2B and B2C Customers */
SELECT
      * 
FROM sales
WHERE `B2B`='TRUE'
;
~~~

~~~ SQL
SELECT
      * FROM sales 
WHERE `B2B`='FALSE';
~~~

~~~ SQL
/* Distribution of B2B and B2C Customers */
SELECT
      `B2B`,
      COUNT(`B2B`)'Count B2B'
FROM sales
WHERE `B2B` IS NOT NULL
GROUP BY `B2B`
ORDER BY `B2B`
;
~~~

~~~ SQL
/* Orders Fulfilment */
SELECT
	  Fulfilment,
      COUNT('Order ID')'Order Fulfilment'
FROM sales
GROUP BY Fulfilment
ORDER BY Fulfilment
;
~~~

~~~ SQL
/* Percentage Distribution of Order Fulfilment */
SELECT 
      Fulfilment,
      COUNT('Order ID')'Order Fulfilment',
      CAST((COUNT('Order ID')*100)/(SELECT COUNT('Order ID')FROM sales)
      AS DECIMAL(4,2))'%Of Orders Fulfilled'
FROM sales
GROUP BY Fulfilment
ORDER BY Fulfilment
;
~~~

~~~ SQL
/* Percentage Distribution Of B2B & B2C Customers */
SELECT
      B2B,
      COUNT('Order ID')'Distribution Of B2B',
	  CAST((COUNT(B2B)*100)/(SELECT COUNT('Order ID')FROM sales) 
      AS DECIMAL(4,2))'%Distribution Of B2B'
FROM sales
GROUP BY B2B
;
~~~

~~~ SQL
/* Average Quantity Of Product Ordered */ 
SELECT
      (SUM(Qty)/COUNT(`Order ID`))'Average Quantity Of Product Ordered'
FROM sales
;
~~~

~~~ SQL
/* The most Common Promotion */
SELECT 
      MAX(`promotion-ids`)'Common Promotion'
FROM sales
;
~~~

~~~ SQL
/* Effectiveness of Promotion To Generate Revenue */
SELECT 
      `promotion-ids`, 
      CAST(SUM(amount) AS SIGNED)Revenue
FROM sales
GROUP BY `promotion-ids`
ORDER BY Revenue
DESC
LIMIT 10
;
~~~

~~~ SQL
/* Checking Revenue For Each Quater */ 
SELECT
      MONTHMANE(date),
      CAST(SUM(amount) 
      AS SIGNED)Revenue 
FROM sales
WHERE QUARTER(date)='2'
GROUP BY MONTHNAME(date)
ORDER BY MONTHNAME(date)
DESC
;
~~~

~~~ SQL
/* Products with high Return or Cancel */ 
SELECT
      category,
      count(`status` = 'Cancelled')'Cancelled Order'
FROM sales
GROUP BY Category
;
~~~

~~~ SQL
/* Products with Return or Cancel Rate */ 
SELECT 
      category,
      COUNT(`status` = 'Cancelled')'Cancelled Order',
      CAST(COUNT(`status` = 'Cancelled') * 100/(SELECT COUNT(`Order ID`) FROM sales) 
      AS DECIMAL(5,3))'Cancelled Or Return Rate'  
FROM sales
GROUP BY category
;
~~~

~~~ SQL
/* Joining Tables To Check Other Products Category & Color */
SELECT
	  sales.index,
      sales.`Order ID`,
      sales.Date,
      report.stock,
      report.category,
      report.size,
      report.color
FROM sales 
JOIN report ON sales.index=report.index
;
~~~

~~~ SQL
/* Creating View For The New Table (Salesview) */
CREATE VIEW Salesview 
AS 
SELECT 
      sales.index,
      sales.`Order ID`,
      sales.Date,
      report.stock,
      report.category,
      report.size,
      report.color
FROM sales JOIN report ON sales.index=report.index
;
~~~

~~~ SQL
SELECT 
* 
FROM Salesview
;
~~~

~~~ SQL
/* Taking Stock Of Product Category and Size */  
SELECT 
      category,
      size,
      COUNT(stock)Stock
FROM salesview
GROUP BY category
ORDER BY stock DESC
;
~~~

~~~ SQL
/* Most Popular or Preferred Color By Product Category */
SELECT 
      category,
      MAX(color)Color
FROM salesview
GROUP BY category
ORDER BY Color
DESC
;
~~~

~~~ SQL
/* Most Popular Color */
SELECT 
      MAX(color)
FROM salesview
;
~~~
