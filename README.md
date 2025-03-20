# Pizza Sales Analysis Project

## Overview  
Analyzed sales data for a pizza chain to identify trends, top-selling products, and customer behavior.  
**Objective:** Optimize inventory, pricing, and marketing strategies using SQL and Excel.

## Tools Used  
- **SQL:** Data extraction, aggregation, and cleaning.  
- **Excel:** Advanced formulas (SUMIFS, VLOOKUP), pivot tables, and interactive dashboards.  
- **Visualization:** Charts (bar graphs, heatmaps) to highlight sales performance.  

## Key Insights  
- Identified **top 5 best-selling pizzas** contributing to 28% of total revenue.  
- Discovered **peak sales hours** (12 PM–2 PM, 6 PM–8 PM) for targeted promotions.  
- Recommended renegotiating supplier contracts for low-selling pizza categories.  

## How to Use This Repository  
1. Download the dataset (`Data/pizza_sales.csv`).  
2. Run SQL scripts (`Code/sales_analysis.sql`) to replicate the analysis.  
3. Open the Excel dashboard (`Output/dashboard.xlsx`) for interactive visuals.  

## Preview  
PIZZA SALES SQL QUERIES
A. KPI’s
1. Total Revenue:
SELECT
  SUM(total_price) AS Total_Revenue
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`;
 ![image](https://github.com/user-attachments/assets/ec8f76e0-dc7f-4f6a-b121-7715504bb8e0)

2. Average Order Value
SELECT
  SUM(total_price) / COUNT (DISTINCT order_id) AS Avg_Order_value
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`;
![image](https://github.com/user-attachments/assets/5f20ea49-134e-4b4c-bd6e-5a9cb8739547)

 
3. Total Pizzas Sold
SELECT
  SUM(quantity) AS Total_pizza_sold
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`;
 ![image](https://github.com/user-attachments/assets/6f6771f3-846b-4f65-96b3-439ec93923ba)
 


4. Total Orders
SELECT
  COUNT(DISTINCT order_id) AS Total_Orders
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`;
  ![image](https://github.com/user-attachments/assets/f44287bb-6612-4ce3-980b-72dc3efdd745)

SELECT
  CAST(SUM(quantity) AS FLOAT64) / 
CAST(COUNT(DISTINCT order_id) AS FLOAT64)
AS Avg_Pizzas_per_order
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`;
![image](https://github.com/user-attachments/assets/6bc3bf00-359e-4878-8552-3aba8177868b)

  
B. Daily Trend for Total Orders
--Daily Trend
SELECT
  FORMAT_DATE('%A', order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`
  GROUP BY order_day
  ORDER BY order_day;
Output:
 ![image](https://github.com/user-attachments/assets/593aa962-021a-4074-902a-68a8ee06de04)

C. Hourly Trend for Orders
--Hourly Trend
SELECT
  EXTRACT(HOUR FROM order_time) AS order_hour, COUNT(DISTINCT order_id) AS total_orders 
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`
  GROUP BY order_hour
  ORDER BY order_hour;
Output
 ![image](https://github.com/user-attachments/assets/9af81dbc-56fa-424e-8235-d54b933b0318)

D. % of Sales by Pizza Category
SELECT pizza_category,sum(total_price)as Total_sales, sum(total_price)*100/(SELECT sum(total_price) from `quixotic-vent-446704-g6.Piza_DB.Pizza_sales` WHERE EXTRACT(MONTH FROM order_date) = 1)  AS PCT
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`
  WHERE EXTRACT(MONTH FROM order_date) = 1
  GROUP BY pizza_category
 
Output
 ![image](https://github.com/user-attachments/assets/d89386af-1172-4e85-835c-d45696a00ead)

E. % of Sales by Pizza Size
SELECT
  pizza_size,
  CAST(SUM(total_price) AS NUMERIC) AS Total_Sales,
  CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM `quixotic-vent-446704-g6.Piza_DB.Pizza_sales` WHERE EXTRACT(QUARTER FROM order_date) = 1) AS NUMERIC) AS PCT
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`
WHERE
  EXTRACT(QUARTER FROM order_date) = 1
GROUP BY
  pizza_size
ORDER BY
  PCT DESC;
Output
 ![image](https://github.com/user-attachments/assets/346839c6-b4d6-4937-acaf-e5f7b40f884a)


F. Total Pizzas Sold by Pizza Category
SELECT
  pizza_category, sum(quantity) AS Total_pizzas_sold
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`
  GROUP BY pizza_category
Output
 ![image](https://github.com/user-attachments/assets/e545b326-f11b-4444-913f-a8e1df55a264)

G. Top 5 Best Sellers by Total Pizzas Sold
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
LIMIT 5;
Output
 ![image](https://github.com/user-attachments/assets/88a58dc4-ac29-41bf-8ebb-9d336e668f2f)





H. Bottom 5 Best Sellers by Total Pizzas Sold
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM
  `quixotic-vent-446704-g6.Piza_DB.Pizza_sales`
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
LIMIT 5;
Output
![image](https://github.com/user-attachments/assets/b020c4d6-0809-47ae-b2c5-1b3487c273f7)
 

