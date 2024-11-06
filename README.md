## SALES PERFORMANCE ANALYSIS OF TEMMYTEE RETAIL STORE

## PROJECT OVERVIEW: This data analysis project aims to generate insights into the Sales Performance of TemmyTee Retail Store over the past year. By analysing the various parameters in the data received, we seek to explore Sales data to uncover key insights such as Top-selling products, Regional performance and Monthly sales trend. The goal is to tell a compelling story by building an interactive dashboard report to gather insight and make business decisions.

## DATA SOURCE: The primary source of data is LITA Capstone dataset.xlsx.

## TOOLS: 
- Microsoft Excel for data cleaning and analysis [download here]()
- Structured Query Language (SQL) for querying of data
- Power BI for Visualization
- GitHub for Portfolio building

## DATA CLEANING AND PREPARATION
At the initial stage of data cleaning and preparation, the following actions were performed;
1. Data loading and inspection
2. Handling missing variables
3. Removing duplicates
4. Data cleaning and formatting

## Exploratory Data Analysis
Some questions were answered on the data as follows;
-  What is the sales overview?
-  What are the Top-performing products?
-  What is the regional breakdown?

## Data Analysis
Calculating Total Sales:
After cleaning the data, I proceeded to calculate the total sales for each transaction by multiplying the quantity by the unit price. This step provided a more comprehensive view of total revenue.

Sales Analysis with Pivot Table:
Next, I created a Pivot Table in Excel to analyze the sales performance. This allowed me to group sales data by:

Category
Product
Region
Month 
The Pivot Table was essential for uncovering trends and gaining insights into sales patterns across different dimensions.

image

## SQL Analysis on Sales Data
Overview
This provides an analysis of sales data using SQL. Each query addresses a specific aspect of the sales performance.

Total sales for each product category
SELECT product, SUM(Total_sale) AS Total_sale
FROM SalesData
GROUP BY product;
Number of sales transactions in each region
SELECT region, COUNT(*) AS transaction_count
FROM SalesData
GROUP BY region;
Highest-selling product by total sales value
SELECT TOP 1 product, SUM(Total_sale) AS total_sales
FROM SalesData
GROUP BY product
ORDER BY total_sales DESC;
Total revenue per product
SELECT product, SUM(Total_sale) AS total_revenue
FROM SalesData
GROUP BY product;
Monthly sales totals for the current year
SELECT MONTH(Orderdate) AS month,
SUM(Total_sale) AS total_sales
FROM SalesData
WHERE YEAR(Orderdate) = 2024
GROUP BY MONTH(Orderdate)
ORDER BY MONTH(Orderdate);
Top 5 customers by total purchase amount
SELECT TOP 5 customer_id, SUM(Total_sale) AS total_purchase
FROM SalesData
GROUP BY customer_id
ORDER BY total_purchase DESC;
Percentage of total sales contributed by each region
SELECT region,
SUM(Total_sale) AS total_sales,
(SUM(Total_sale) / (SELECT SUM(Total_sale) FROM SalesData) * 100) AS percentage_of_total_sales
FROM SalesData
GROUP BY region;
Products with no sales in the last quarter
SELECT product 
FROM SalesData
GROUP BY product
HAVING SUM(CASE WHEN Orderdate BETWEEN '2024-06-01' AND '2024-08-31' THEN 1 ELSE 0 END) = 0;
-- ========================== -- End of SQL Analysis -- ==========================

Visualising Sales Data with Power BI
Power BI Data Preparation
Imported the dataset into Power BI.
Corrected the data types for accuracy.
Cleaned the data by rearranging the dates to fit the date data type correctly.
Grouped the dates into months for better analysis.
Created a measure to calculate total revenue.
image

Sales Total Revenue & Total Quantity of Products Sold
These metrics offer a high-level overview of the overall sales performance. The Total Revenue ($2,101,090) reflects the financial success, while the Total Quantity of Products Sold (68,461) indicates the volume of products moved. Together, these figures summarize the business’s achievements in terms of revenue generation and product demand.

Sales Distribution by Region (Pie Chart)
This pie chart illustrates the distribution of sales across different regions. The East region leads with 44.16% of total sales, followed by the North region at 23.13%, with other regions contributing smaller shares. This breakdown helps identify regional strengths, allowing the business to focus on high-performing areas or to develop targeted strategies for regions with lower sales.

Top Selling Products (Bar Chart)
This bar chart highlights the best-selling products, with Shoes being the highest-selling item, followed by Shirts and Hats. This insight helps identify the most popular products that drive significant revenue, guiding inventory management and marketing efforts toward these high-demand items.

Quantity Sold by Region (Donut Chart)
The donut chart shows the distribution of product quantities sold by region. It reveals a fairly even distribution, with each region contributing approximately the same share. This balance suggests that demand for products is relatively uniform across all regions.

Quantity of Product Sold by Month (Stacked Bar Chart)
This chart shows the monthly sales breakdown of products, highlighting seasonal demand variations.

Hats peak in sales in March.
Shoes and shirts have consistent demand year-round.
This data aids in inventory and marketing strategy planning.

Conclusion
The sales data analysis showed that:

Top Products: Gloves clear best-sellers.
Regional Strengths: East perform better than others.
Capstone Project 2: Customer Segmentation for a Subscription Service
Objective:
Segment customers based on their subscription behavior, region, and purchase patterns to:

Improve customer retention.
Create targeted marketing strategies.
Optimize subscription plans to boost revenue and customer retention value.
Tools Used:
Excel for data cleaning and analysis.
SQL for querying and data manipulation.
Power BI for visualization and reporting.
Expected Outcomes:
Enhanced customer retention with personalized marketing.
Optimized subscription offerings to drive revenue.
Insights into the most profitable customer segments and regions.
Tools:
Excel
SQL
Power BI
pivot Presentation
Subscription Type Report
This report provides the total number of customers for each subscription type. It highlights customer distribution across different subscription plans, offering insights into popular subscription tiers and customer preferences.

image

Customer Subscription Analysis
Table 1: Active vs. Canceled Customers
This table presents the count of active customers compared to those who have canceled their subscriptions. This data provides an overview of customer retention and cancellation rates.

Table 2: Retention Analysis for 2022 and 2023
The second table dives deeper into customer retention trends by showing:

The number of customers who canceled their subscriptions in 2022 and 2023.
The number of customers who remained active across both years.
These insights help assess the effectiveness of retention efforts and identify patterns in customer loyalty over time.

image

Table 1: Subscription Start Date by Quarter
The first table compares the subscription start date with each quarter of the year. This analysis helps identify trends in customer sign-ups by quarter, revealing any seasonal patterns in subscription activity.

Table 2: Subscription Start Date by Type and Year
The second table provides a comparison of the subscription start date by both subscription type and year. This breakdown offers insights into how different subscription types have trended over time, helping to assess long-term customer preferences.

image

SQL Queries for CUSOMER SEGMENATION FOR A SUBSCRIPTION SERVICE
 Select * from [dbo].[CustomerData]
retrieve the total number of customers from each region.
Select region, count(CustomerID) as Total_number
 from [dbo].[CustomerData]
 group by region
the most popular subscription type by the number of customers
select subscriptionType, count(customerid) as most_Popular
from [dbo].[CustomerData]
group by SubscriptionType
customers who canceled their subscription within 6 months
 select customerid from [dbo].[CustomerData]
 where DATEDIFF(month,subscriptionStart,subscriptionend) <=6
the average subscription duration for all customers.
select avg(datediff(day,subscriptionStart,subscriptionend)) as AverageSubscripionDuration
from [dbo].[CustomerData]
customers with subscriptions longer than 12 months.
 select customerid, subscription_length
 from [dbo].[CustomerData]
 where DATEDIFF(month,subscriptionStart,subscriptionend) > 12
Total revenue by subscription type
from [dbo].[CustomerData]
group by subscriptiontype;
Top 3 regions by subscription cancellations.
from [dbo].[CustomerData]
where canceled = '0'
group by region
order by cancellation desc;
The total number of active and canceled subscriptions
sum(case when canceled= '0' then 1 else 0 end) as cancelled
from [dbo].[CustomerData];
Visualising customer Data with Power BI
Power BI Data Preparation
I_ Imported the dataset into Power BI.
I Corrected the data types for accuracy.
I Cleaned the data by rearranging the dates to fit the date data type correctly.
