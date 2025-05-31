# Pizza Sales Analysis

## Table of Contents 

- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis (EDA) Questions](#exploratory-data-analysis-eda-questions)
- [Data Analysis](#data-analysis)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)


### Project overview 

This project involves analyzing pizza sales data to uncover insights that can guide business decisions and performance evaluation. The goal is to build an interactive dashboard that highlights key performance indicators (KPIs) such as revenue, order value, and sales volume. The analysis focuses on identifying sales trends, customer behavior, and operational metrics to support data-driven strategy in the food service business.


### Problem Statement 

  #### KPI's Requirement 

We need to analyze key indicators for our pizza sales data to gain insights into our business
performance. Specifically, we want to calculate the following metrics:

1. Total Revenue: The sum of the total price of all pizza orders.
2. Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
3. Total Pizzas Sold: The sum of the quantities of all pizzas sold.
4. Total Orders: The total number of orders placed.
5. Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

### Data Sources 

### Tools 
 - Excel for data cleaning
 - Microsoft SQL for data analysis 
 - Power BI - visualization 


### Data Cleaning/Preparation 

1. Data inspection
2. Standardizing formats on the pizza column size replace L with Large, M for Medium an S for Rgular and XLarge to X Large
3. Removing duplicates

### Exploratory Data Analysis (EDA) Questions
1. Sales Trends
  - How does total revenue vary by day, week, or month?
  - Are there seasonal patterns or peak periods in pizza sales?

2. Product Performance
  - Which pizza types or categories generate the most revenue?
  - Which pizzas are ordered most frequently?

3. Customer Behavior

  - What is the distribution of order values?
  - How many pizzas do customers typically order per transaction?

4. Time-Based Insights

  - What times of day or days of the week have the highest order volumes?
  - Are there specific time slots that generate more revenue?

5. Order Composition

  - What is the average number of items per order?
  - Are certain pizza sizes or types often ordered together?

6. Revenue Drivers
  - Is higher revenue driven more by quantity or high-priced items?
  - Are larger orders associated with specific customer segments or time frames?

7. Operational Questions
  - Are there differences in performance across different locations (if applicable)?
  - Are there bottlenecks or outliers in the order processing or delivery data?

### Data Analysis 
  ### KPI's
  
Total Revenue

`SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;`

Average Order Value 

`SELECT SUM(total_price)/ COUNT (DISTINCT order_id) AS Average_Order_Value from pizza_sales `

Total Number of Pizzas Sold

`SELECT SUM(quantity) As Total_Pizza_Sold from pizza_sales`

Total_Orders

`SELECT COUNT (DISTINCT order_id) As Total_Orders from pizza_sales`

Average Pizzas Per Order

`SELECT CAST( CAST (SUM(quantity) AS decimal (10,2)) / 
CAST(COUNT (Distinct order_id)AS decimal (10,2))as decimal (10,2)) AS Average_Pizzas_per_order from pizza_sales`


Total oders by day of week 

`SELECT DATENAME(DW, order_date)as order_day, COUNT (DISTINCT order_id) AS Total_orders
from pizza_sales 
GROUP BY DATENAME (DW, order_date)`

Total oders by month

`SELECT DATENAME(MONTH, order_date)as Month_name, COUNT (DISTINCT order_id) AS Total_orders
from pizza_sales 
GROUP BY DATENAME (MONTH, order_date)`


Percentage of Sales by Pizza Category

`SELECT pizza_category,sum(total_price) as total_sales, sum(total_price) * 100 / (SELECT sum(total_price) from pizza_sales) AS Percentage_of_sales
from pizza_sales
GROUP BY pizza_category`

Percentage of Sales by Pizza Size

`SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER  BY PCT DESC`

Total Revenue from top five types of pizza 

`SELECT TOP 5 pizza_name, Sum (total_price) as Total_Revenue FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC`

Top selling Pizza by numbers

`SELECT TOP 5 pizza_name, Sum (quantity) as Total_quantity FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_quantity DESC`

## Results/Findings 


### Recommendations

### Limitations

