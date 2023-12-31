## Pizza-Sales-Dashboard
This project analyzes key performance indicators form a pizza sales data to gain insights into the business performance such as sales performance, customer spending behavior, and operational efficiency. This was done by creating KPI's and Charts on a Dashboard in Power BI with SQL connection.

## Table of content

## PROBLEM STATEMENT
### KPI Requirements
To analyze key indicators form a pizza sales data to gain insights into the business performance. we want to calculate the following metrics:
1.	Total Revenue: The sum of the total price of all pizza orders.
2.	Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
3.	Total Pizzas Sold: The sum of the quantities of all pizzas sold.
4.	Total Orders: The total number of orders placed.
5.	Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

These KPIs will help in understanding sales performance, customer spending behavior, and operational efficiency.

### Charts Requirements
To visualize various aspects of the pizza sales data to gain insights and understand key trends. Need to identify the following requirements for creating the charts:
1.	Daily Trend for Total Orders:
    -	Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.
2.	Monthly Trend for Total Orders:
    -	Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.
3.	Percentage of Sales by Pizza Category:
    -	Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

These charts are designed to provide a visual representation of sales trends and category performance, which can inform business decisions and strategy adjustments.

## SOFTWARES USED TO DEVELOPTHE REPORT
  - Power BI - Version: 2.116.966.0, 64-bit
  - MS SQL Server – 19.0.2
  - Excel 

## DATA SOURCE
The primary dataset was obtained from Kaggle website (https://www.kaggle.com/datasets/ylenialongo/pizza-sales) 

## IMPORT DATA INTO MS SQL SERVER
The datasets were imported into the Microsoft SQL server to query the data according to our KPI and chart requirements. The results served as check on the Power BI analysis. Some of the queries are shown below.

### SQL Queries
```
-- Total Revenue:
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

-- Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)

-- % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category

-- Top 5 Pizzas by Revenue
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC

-- Borrom 5 Pizzas by Total Orders
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
```

## CONNECTING POWER BI TO MS SQL Database
Power BI was connected to MS SQL Database for Exploratory Data Analysis and building of the Dashboard.

### Power BI Functionalities Used
-	How to connect Power BI to MS SQL server and Flat Files
-	Data cleaning in Power Query
-How to create a Date Table in Power BI
-	Creating Dynamic and Complex KPI’s
-	Basic to Advanced Dax Queries
-Conditional Formatting's
-Creating different charts and formatting them

### DAX Queries

```
Aveg pizza per order = [Total pizzas sold]/[Total orders]

Avg order value = [Total Revenue]/[Total orders]

order_day = UPPER(LEFT(pizza_sales[Day Name], 3))

order_month = UPPER(LEFT(pizza_sales[Month Name], 3))

Total orders = DISTINCTCOUNT(pizza_sales[order_id])

Total pizzas sold = SUM(pizza_sales[quantity])

Total Revenue = SUM(pizza_sales[total_price])
```
	
## VISUALIZATION AND DASHBOARD
The final dashboards are shown below:
### The Home page
![image](https://github.com/Fkuukyee/Pizza-Sales-Dashboard/assets/147086232/34e292fe-b144-47ee-bd2e-489b9e04ecb0)

### The Best/Worst sellers page
![image](https://github.com/Fkuukyee/Pizza-Sales-Dashboard/assets/147086232/c2d43d04-5d95-4091-920c-2d35e215c02d)


## INSIGHTS
Based on the analysis of the pizza sales data, the following insights were gleaned:
-	Total Revenue: $817,860.05
-	Average Order Value: $38.31
-	Total Pizzas Sold: 49,574 pizzas
-	Total Orders: 21,350 orders
-	Average Pizzas Per Order: 2.32 pizzas per order
-	Best Days: Orders are highest on Wednesdays, Fridays and Saturdays.
-	Best Months: There are maximum orders for the month of July and January
-	Category: The Classic category contributed to the highest sales and total orders
-	Size: The Large size pizza contributes to the maximum sales
-	Total Revenue: The Thai Chicken pizza contributes to the maximum Revenue whilst the Brie Carre Pizza contributes to minimum Total Revenue
-	Total Quantity: The Classic Deluxe Pizza gives the maximum Total Quantity whiles the Brie Carre Pizza Contributes to minimum Total Quantity
-	Total Orders: The Classic Deluxe Pizza Contributes to maximum Total orders whiles the Spicy Italian Pizza Contributes to minimum Total orders


