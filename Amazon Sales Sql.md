~~~ SQL
SELECT * 
FROM sales;
~~~

~~~ SQL
/* Revenue */ 
SELECT 
      CAST(SUM(amount) 
      AS SIGNED)Revenue
FROM sales;
~~~
| Revenue  |
|----------|
| 78592678 |

~~~ SQL
/* Sales Quantity */
SELECT 
      SUM(Qty)'Sales Quantity' 
FROM sales;
~~~
| Sales Quantity |
|----------------|
| 116649         |

~~~ SQL
/* Total Orders */
SELECT 
      COUNT('Order ID')'Total Orders'
FROM sales;
~~~
| Total Orders |
|--------------|
| 128975       |
|              |
~~~ SQL
/* Average Order Value */
SELECT 
      CAST(SUM(amount)/COUNT('Order ID') 
      AS DECIMAL (7,2))'Average Order Value' 
FROM sales;
~~~
| Average Order Value |
|---------------------|
| 609.36              |
|                     |

~~~ SQL
/* The highest product ordered by category */
SELECT 
      MAX(category)Product 
FROM sales;
~~~
| Product       |
|---------------|
| Western Dress |

~~~ SQL
/* Top 5 products ordered(Most Popular) */
SELECT 
      MAX(category)'Most Popular Product'
FROM sales
GROUP BY category
ORDER BY category 
DESC
LIMIT 5;
~~~
| Most Popular Product |
|----------------------|
| Western Dress        |
| Top                  |
| Set                  |
| Saree                |
| kurta                |
|                      |

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
DESC;
~~~ 
| Month | Revenue  |
|-------|----------|
| April | 28838708 |
| May   | 26226477 |
| June  | 23425809 |
| March | 101684   |
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
LIMIT 1;
~~~
| Month | Revenue  |
|-------|----------|
| April | 28838708 |

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
ASC;
~~~
| Days | Revenue |
|------|---------|
| 1    | 2880866 |
| 2    | 2982101 |
| 3    | 2940626 |
| 4    | 2983899 |
| 5    | 2834341 |
| 6    | 2751792 |
| 7    | 2787150 |
| 8    | 2886263 |
| 9    | 2742205 |
| 10   | 2597648 |
| 11   | 2553751 |
| 12   | 2535887 |
| 13   | 2591302 |
| 14   | 2780893 |
| 15   | 2704277 |
| 16   | 2552017 |
| 17   | 2453112 |
| 18   | 2424748 |
| 19   | 2467922 |
| 20   | 2553599 |
| 21   | 2474228 |
| 22   | 2534502 |
| 23   | 2504197 |
| 24   | 2472292 |
| 25   | 2451478 |
| 26   | 2451979 |
| 27   | 2378136 |
| 28   | 2461434 |
| 29   | 2068182 |
| 30   | 1787098 |
| 31   | 1004753 |

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
LIMIT 3;
~~~
| Days | Revenue |
|------|---------|
| 4    | 2983899 |
| 2    | 2982101 |
| 3    | 2940626 |

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
LIMIT 5;
~~~
| category      | Revenue     |
|---------------|-------------|
| Set           | 39204124.03 |
| kurta         | 21299546.7  |
| Western Dress | 11216072.69 |
| Top           | 5347792.3   |
| Ethnic Dress  | 791217.66   |

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
ORDER BY Revenue DESC;
~~~
| category      | Revenue     | %By Category |
|---------------|-------------|--------------|
| Set           | 39204124.03 | 49.883       |
| kurta         | 21299546.7  | 27.101       |
| Western Dress | 11216072.69 | 14.271       |
| Top           | 5347792.3   | 6.804        |
| Ethnic Dress  | 791217.66   | 1.007        |
| Blouse        | 458408.18   | 0.583        |
| Bottom        | 150667.98   | 0.192        |
| Saree         | 123933.76   | 0.158        |
| Dupatta       | 915         | 0.001        |

~~~ SQL
/* Revenue By Size */
SELECT 
      size,
      CAST(SUM(amount)
      AS DECIMAL (10,2)) Revenue 
FROM sales
GROUP BY size
ORDER BY Revenue
DESC;
~~~
| size | Revenue     |
|------|-------------|
| M    | 13906754.37 |
| L    | 13234886.19 |
| XL   | 12464965.86 |
| XXL  | 10636288.45 |
| S    | 10629210.18 |
| 3XL  | 9157147.68  |
| XS   | 7022375.2   |
| 6XL  | 576249.33   |
| 5XL  | 425156.63   |
| 4XL  | 334451.64   |
| Free | 205192.77   |

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
DESC;
~~~
| size | Revenue     | %By Size |
|------|-------------|----------|
| M    | 13906754.37 | 17.69    |
| L    | 13234886.19 | 16.84    |
| XL   | 12464965.86 | 15.86    |
| XXL  | 10636288.45 | 13.53    |
| S    | 10629210.18 | 13.52    |
| 3XL  | 9157147.68  | 11.65    |
| XS   | 7022375.2   | 8.94     |
| 6XL  | 576249.33   | 0.73     |
| 5XL  | 425156.63   | 0.54     |
| 4XL  | 334451.64   | 0.43     |
| Free | 205192.77   | 0.26     |

~~~ SQL
/* Top Citys By Revenue */
SELECT
	  `ship-city`,
      CAST(SUM(amount) AS SIGNED)Revenue 
      FROM sales
GROUP BY `ship-city`
ORDER BY Revenue 
DESC
LIMIT 5;
~~~
| ship-city | Revenue |
|-----------|---------|
| BENGALURU | 7257749 |
| HYDERABAD | 5599822 |
| MUMBAI    | 4293210 |
| NEW DELHI | 3952690 |
| CHENNAI   | 3606918 |

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
LIMIT 10;
~~~
| ship-city | Revenue | %By Ship-city |
|-----------|---------|---------------|
| BENGALURU | 7257749 | 9.23          |
| HYDERABAD | 5599822 | 7.13          |
| MUMBAI    | 4293210 | 5.46          |
| NEW DELHI | 3952690 | 5.03          |
| CHENNAI   | 3606918 | 4.59          |
| pune      | 2794976 | 3.56          |
| KOLKATA   | 1682047 | 2.14          |
| GURUGRAM  | 1280855 | 1.63          |
| THANE     | 1111506 | 1.41          |
| LUCKNOW   | 1049983 | 1.34          |

~~~ SQL
/* Top States By Order */
SELECT
      `ship-state`,
      COUNT(`Order ID`)`Count Order ID` 
FROM sales
GROUP BY `ship-state`
ORDER BY `Count Order ID`
DESC
LIMIT 10;
~~~
| ship-state     | Count Order ID |
|----------------|----------------|
| MAHARASHTRA    | 22260          |
| KARNATAKA      | 17326          |
| TAMIL NADU     | 11483          |
| TELANGANA      | 11330          |
| UTTAR PRADESH  | 10638          |
| DELHI          | 6967           |
| KERALA         | 6585           |
| WEST BENGAL    | 5963           |
| ANDHRA PRADESH | 5430           |
| Gujarat        | 4489           |

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
LIMIT 10;
~~~
| ship-state     | Count Order ID | %Order Contribution |
|----------------|----------------|---------------------|
| MAHARASHTRA    | 22260          | 17.26               |
| KARNATAKA      | 17326          | 13.43               |
| TAMIL NADU     | 11483          | 8.9                 |
| TELANGANA      | 11330          | 8.78                |
| UTTAR PRADESH  | 10638          | 8.25                |
| DELHI          | 6967           | 5.4                 |
| KERALA         | 6585           | 5.11                |
| WEST BENGAL    | 5963           | 4.62                |
| ANDHRA PRADESH | 5430           | 4.21                |
| Gujarat        | 4489           | 3.48                |

~~~ SQL
/* Top States By Revenue */
SELECT
      `ship-state`,
      CAST(SUM(amount) AS SIGNED)Revenue FROM sales
GROUP BY `ship-state`
ORDER BY Revenue
DESC
LIMIT 10;
~~~
| ship-state     | Revenue  |
|----------------|----------|
| MAHARASHTRA    | 13335534 |
| KARNATAKA      | 10481114 |
| TELANGANA      | 6916616  |
| UTTAR PRADESH  | 6816642  |
| TAMIL NADU     | 6515650  |
| DELHI          | 4346412  |
| KERALA         | 3830228  |
| WEST BENGAL    | 3507880  |
| ANDHRA PRADESH | 3219832  |
| HARYANA        | 2882093  |

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
LIMIT 10;
~~~
| ship-state     | Revenue  | %By Ship-state |
|----------------|----------|----------------|
| MAHARASHTRA    | 13335534 | 16.97          |
| KARNATAKA      | 10481114 | 13.34          |
| TELANGANA      | 6916616  | 8.8            |
| UTTAR PRADESH  | 6816642  | 8.67           |
| TAMIL NADU     | 6515650  | 8.29           |
| DELHI          | 4346412  | 5.53           |
| KERALA         | 3830228  | 4.87           |
| WEST BENGAL    | 3507880  | 4.46           |
| ANDHRA PRADESH | 3219832  | 4.1            |
| HARYANA        | 2882093  | 3.67           |

~~~ SQL
/* Shows the Cancelled Ordered */
SELECT * 
FROM sales 
WHERE  `Status`= 'Cancelled';
~~~

~~~ SQL
/* Trends in Order Cancellation */
SELECT 
      `Status`,
      COUNT(`Status`= 'Cancelled')`Cancelled-Order` 
FROM sales
GROUP BY `Status`
ORDER BY `Cancelled-Order`
DESC;
~~~
| Status                        | Cancelled-Order |
|-------------------------------|-----------------|
| Shipped                       | 77804           |
| Shipped - Delivered to Buyer  | 28769           |
| Cancelled                     | 18332           |
| Shipped - Returned to Seller  | 1953            |
| Shipped - Picked Up           | 973             |
| Pending                       | 658             |
| Pending - Waiting for Pick Up | 281             |
| Shipped - Returning to Seller | 145             |
| Shipped - Out for Delivery    | 35              |
| Shipped - Rejected by Buyer   | 11              |
| Shipping                      | 8               |
| Shipped - Lost in Transit     | 5               |
| Shipped - Damaged             | 1               |

~~~ SQL
/* To Check B2B and B2C Customers */
SELECT * 
FROM sales
WHERE `B2B`='TRUE';
~~~

~~~ SQL
SELECT *
FROM sales 
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
ORDER BY `B2B`;
~~~
| B2B   | Count B2B |
|-------|-----------|
| FALSE | 128104    |
| TRUE  | 871       |

~~~ SQL
/* Orders Fulfilment */
SELECT
      Fulfilment,
      COUNT('Order ID')'Order Fulfilment'
FROM sales
GROUP BY Fulfilment
ORDER BY Fulfilment;
~~~
| Fulfilment | Order Fulfilment |
|------------|------------------|
| Amazon     | 89698            |
| Merchant   | 39277            |

~~~ SQL
/* Percentage Distribution of Order Fulfilment */
SELECT 
      Fulfilment,
      COUNT('Order ID')'Order Fulfilment',
      CAST((COUNT('Order ID')*100)/(SELECT COUNT('Order ID')FROM sales)
      AS DECIMAL(4,2))'%Of Orders Fulfilled'
FROM sales
GROUP BY Fulfilment
ORDER BY Fulfilment;
~~~
| Fulfilment | Order Fulfilment | %Of Orders Fulfilled |
|------------|------------------|----------------------|
| Amazon     | 89698            | 69.55                |
| Merchant   | 39277            | 30.45                |

~~~ SQL
/* Percentage Distribution Of B2B & B2C Customers */
SELECT
      B2B,
      COUNT('Order ID')'Distribution Of B2B',
	  CAST((COUNT(B2B)*100)/(SELECT COUNT('Order ID')FROM sales) 
      AS DECIMAL(4,2))'%Distribution Of B2B'
FROM sales
GROUP BY B2B;
~~~
| B2B   | Distribution Of B2B | %Distribution Of B2B |
|-------|---------------------|----------------------|
| FALSE | 128104              | 99.32                |
| TRUE  | 871                 | 0.68                 |

~~~ SQL
/* Average Quantity Of Product Ordered */ 
SELECT
      (SUM(Qty)/COUNT(`Order ID`))'Average Quantity Of Product Ordered'
FROM sales;
~~~
| Average Quantity Of Product Ordered |
|-------------------------------------|
| 0.9044                              |

~~~ SQL
/* The most Common Promotion */
SELECT 
      MAX(`promotion-ids`)'Common Promotion'
FROM sales;
~~~
| Common Promotion          |
|---------------------------|
| VPC-44571-44201853 Coupon |

~~~ SQL
/* Effectiveness of Promotion To Generate Revenue */
SELECT 
      `promotion-ids`, 
      CAST(SUM(amount) AS SIGNED)Revenue
FROM sales
GROUP BY `promotion-ids`
ORDER BY Revenue
DESC
LIMIT 2;
~~~
| promotion-ids                                | Revenue  |
|----------------------------------------------|----------|
| IN Core Free Shipping 2015/04/08 23-48-5-108 | 31815155 |
| No Promotion                                 | 25004243 |

~~~ SQL
/* Checking Revenue For Each Quater */ 
SELECT
      MONTHNAME(date)Quater,
      CAST(SUM(amount) 
      AS SIGNED)Revenue 
FROM sales
WHERE QUARTER(date)='2'
GROUP BY MONTHNAME(date)
ORDER BY MONTHNAME(date)
DESC;
~~~
| Quater | Revenue  |
|--------|----------|
| May    | 26226477 |
| June   | 23425809 |
| April  | 28838708 |

~~~ SQL
/* Products with high Return or Cancel */ 
SELECT
      category,
      count(`status` = 'Cancelled')'Cancelled Order'
FROM sales
GROUP BY Category;
~~~
| category      | Cancelled Order |
|---------------|-----------------|
| Set           | 50284           |
| kurta         | 49877           |
| Western Dress | 15500           |
| Top           | 10622           |
| Ethnic Dress  | 1159            |
| Bottom        | 440             |
| Saree         | 164             |
| Blouse        | 926             |
| Dupatta       | 3               |

~~~ SQL
/* Products with Return or Cancel Rate */ 
SELECT 
      category,
      COUNT(`status` = 'Cancelled')'Cancelled Order',
      CAST(COUNT(`status` = 'Cancelled') * 100/(SELECT COUNT(`Order ID`) FROM sales) 
      AS DECIMAL(5,3))'Cancelled Or Return Rate'  
FROM sales
GROUP BY category;
~~~
| category      | Cancelled Order | Cancelled Or Return Rate |
|---------------|-----------------|--------------------------|
| Set           | 50284           | 38.987                   |
| kurta         | 49877           | 38.672                   |
| Western Dress | 15500           | 12.018                   |
| Top           | 10622           | 8.236                    |
| Ethnic Dress  | 1159            | 0.899                    |
| Bottom        | 440             | 0.341                    |
| Saree         | 164             | 0.127                    |
| Blouse        | 926             | 0.718                    |
| Dupatta       | 3               | 0.002                    |

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
JOIN report ON sales.index=report.index;
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
FROM sales JOIN report ON sales.index=report.index;
~~~

~~~ SQL
SELECT * 
FROM Salesview;
~~~

~~~ SQL
/* Taking Stock Of Product Category and Size */  
SELECT 
      category,
      size,
      COUNT(stock)Stock
FROM salesview
GROUP BY category
ORDER BY stock
DESC
LIMIT 10;
~~~
| category      | size | Stock |
|---------------|------|-------|
| KURTA         | L    | 3726  |
| KURTA SET     | L    | 1598  |
| SET           | L    | 1050  |
| TOP           | L    | 865   |
| DRESS         | L    | 700   |
| BLOUSE        | FREE | 241   |
| NIGHT WEAR    | XXL  | 217   |
| TUNIC         | L    | 154   |
| SAREE         | FREE | 147   |
| AN : LEGGINGS | L    | 131   |

~~~ SQL
/* Most Popular or Preferred Color By Product Category */
SELECT 
      category,
      MAX(color)Color
FROM salesview
GROUP BY category
ORDER BY Color
DESC;
~~~
| category             | Color     |
|----------------------|-----------|
| AN : LEGGINGS        | Yellow    |
| DRESS                | Yellow    |
| KURTA SET            | Yellow    |
| SET                  | Yellow    |
| TOP                  | Yellow    |
| KURTA                | Yellow    |
| SAREE                | Yellow    |
| NIGHT WEAR           | Yellow    |
| BLOUSE               | White     |
| PANT                 | White     |
| BOTTOM               | White     |
| PALAZZO              | White     |
| LEHENGA CHOLI        | White     |
| TUNIC                | White     |
| JUMPSUIT             | White     |
| SHARARA              | TEAL BLUE |
| KURTI                | Teal      |
| CROP TOP             | Red       |
| SKIRT                | OFF WHITE |
| CARDIGAN             | Mustard   |
| CROP TOP WITH PLAZZO | Cream     |

~~~ SQL
/* Most Popular Color */
SELECT 
      MAX(color)
FROM salesview;

~~~
| MAX(color) |
|------------|
| Yellow     |

