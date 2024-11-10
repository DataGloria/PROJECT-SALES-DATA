# LITA-CAPSTONE-PROJECT-SALES-DATA-
# Sales Performance Analysis for a Retail Store

TABLE OF CONTENTS

[Project Overview](#project-overview)

[Project Summary](#project-summary)

[Project Structure](#project-structure)

[Excel Analysis](#excel-analysis)

[SQL Analysis](#sql-analysis)

[Power BI Dashboard](#power-bi-dashboard)

[Key Insights](#key-insights)


### Project Overview
This project involves analyzing the sales performance of a retail store to uncover valuable insights. The analysis spans three primary tools—Excel, SQL, and Power BI—and focuses on identifying trends in product sales, regional performance, and monthly sales, with the final output visualized in an interactive Power BI dashboard.

---

## Project Summary

- **Objective**: To analyze sales data for a retail store, identify top-selling products, examine regional and monthly trends, and provide actionable insights.
- **Tools Used**: Microsoft Excel, SQL Server, Power BI
- **Outcome**: An interactive Power BI dashboard that visualizes the sales overview, trends, top products, and regional performance.

---

## Project Structure

1. ### Excel Analysis: [View Here](https://docs.google.com/spreadsheets/d/1yjZ7dtWELhHT4SZxeZ3UnsTnEFzvt6F2/edit?usp=sharing&ouid=101772182884448801883&rtpof=true&sd=true)
   - **Initial Exploration**: Explored sales data using pivot tables for summarizing;
      - total sales by product,
      - total sales by region,
      - Total sales per month
      - Sum of revenue per product
      - Average Unit price of each product
      - Sum of revenue per product over the years analyzed, and
      - Product trends over the years (Quantity sold). This includes a slicer to gain better understanding per product
   - **Metric Calculations**:
     - Calculated average sales per product and total revenue by region.
     - Total revenue per region
       

2. **SQL Analysis**: [View Here](https://drive.google.com/file/d/1y1eAeoNXLUbWVF76y5wo9XMWiC8oj1UO/view?usp=sharing)
   - **Dataset Loading**: Loaded the dataset into SQL Server for deeper analysis anad cleaned the data
   - **Key Queries**:
     - **Total Sales by Product Category**:
       ```sql
       SELECT Product, 
       SUM(Quantity) AS Total_sales
       FROM [dbo].[Sales data Cp]
       GROUP BY Product;

       ```
     - **Number of Sales Transactions by Region**:
       ```sql
       SELECT Region, 
       SUM(Quantity) AS Number_of_sales_Transaction
       FROM [dbo].[Sales data Cp]
       GROUP BY Region;

       ```
     - **Highest-Selling Product**:
       ```sql
       SELECT Product,
       SUM (Total_Revenue) as Total_sales_value
       FROM [dbo].[Sales data Cp]
       GROUP BY PRODUCT
       ORDER BY Total_sales_value DESC;
       ```
     - **Revenue per Product**:
       ```sql
       SELECT Product,
       SUM (Total_Revenue) as Total_revenue_per_product
       FROM [dbo].[Sales data Cp]
       GROUP BY PRODUCT
       ORDER BY Total_revenue_per_product DESC;
       ```
     - **Monthly Sales Totals**:
       ```sql
       SELECT MONTH(OrderDate) AS Month_name, 
       SUM(Quantity) AS Total_Sales
       FROM [dbo].[Sales data Cp]
       WHERE YEAR(OrderDate) = YEAR(GETDATE())
        GROUP BY MONTH(OrderDate)
        ORDER BY Month_name;
       ```
     - **Top 5 Customers by Purchase Amount**:
       ```sql
       SELECT Top 5 customer_id,
        SUM (Total_revenue) AS  Total_purchase_amount
        FROM [dbo].[Sales data Cp]
        GROUP BY Customer_id
        ORDER BY Total_purchase_amount DESC;

       ```
     - **Sales Contribution by Region**:
       ```sql
       WITH TotalSales AS (
        SELECT SUM(Quantity) AS Overall_Sales
         FROM [dbo].[Sales data Cp]
         )
          SELECT Region, 
       SUM(Quantity) AS Region_Sales, 
       CAST(ROUND((SUM(Quantity) * 100.0 / (SELECT Overall_Sales FROM TotalSales)), 0) AS VARCHAR(10)) + '%' AS Sales_Percentage
        FROM [dbo].[Sales data Cp]
        GROUP BY Region
        ORDER BY Sales_Percentage DESC;

       ```
     - **Products with No Sales in Last Quarter**:
       ```sql
       SELECT DISTINCT Product
        FROM [dbo].[Sales data Cp]
       WHERE Product NOT IN (
               SELECT Product
               FROM [dbo].[Sales data Cp]
                WHERE OrderDate >= DATEADD(QUARTER, -1, GETDATE())
       ```
   

3. **Power BI Dashboard**:[View Here](https://drive.google.com/file/d/1Ja7vrT2m-xvI-uMTwzHCdA65wqOHLY0s/view?usp=sharing)
   - **Overview**: I Created an interactive dashboard summarizing key insights which is guaranteed to help the company see patterns and trends that will improve key decision making and overall, help the business identify areas, products to improve on, incease marketability or highlight.
      - transaformed the data by chnaging the data types as related to the values or texts in the columns
      - Performed a data audit to check if the data quality was topnotch
      - created measures and calculated colums to visualized average quantiy, average unit price and count of customers
   - **Visualizations**:
     - **Sales Overview**: Displays total sales, average quantity sold, and the total sales made ( total time customers ordered from us)
       
     - **Top Products**: this highlights the best-selling products by total revenue which was repreaented by a column chart
       
     - **Regional Breakdown**: This visualizes the sales contribution by each region and top-performing regions. knowing this will help the client concetrate on regions that are high performing while taking steps to impreove on low performing regions. Steps could include research on reasons for low sales, improving and increasing product promotion or taking feedbacks from customers to improve on product design e.t.c.

   - **Dashboard Preview**:
      (continuation) This dashboard also provides a comprehensive analysis of the dataset, including:

      - **Quantity Overview**: We provide a display of  total quantity by product and region, with a percentage breakdown of quantity by region to show the percentage contribution of each region to the ttal product
      - **Customer Revenue**: this visualization Shows revenue per customer by region, highlighting top-performing regions and revenue distribution.
      - **Monthly Revenue Trends**: We provide a visualizatio of the analysis of monthly revenue totals, identifying highest and lowest performing months with icons representing the highest performing months where the company realised a total sales of over $100,000, Mid revenue greater than $50,000 but less than $100,000 nand low performing months where the company realised less than $50,000
      - **Regional Customer Distribution**: Presents customer count by region, offering insights into regional engagement.

    - **Features**:
   
      - **Region-Based Slicers**: Users can filter data by region for a more tailored view.

This dashboard enables users to gain a clear understanding of product and customer performance across various regions and time periods.

     - 
   :![Screenshot 2024-11-10 220427](https://github.com/user-attachments/assets/39a5636c-fa5b-4991-bbcf-bf74f26deaef)



---

## Key Insights

- **Top-Selling Products**: Identified the products with the highest sales value, providing insight into popular items.
- **Regional Performance**: Analyzed which regions contribute the most to overall sales, enabling targeted marketing strategies.
- **Sales Trends**: Monthly and quarterly trends reveal sales seasonality, helping optimize inventory and resource allocation.
- **Customer Insights**: Recognized the top customers by purchase amount, valuable for loyalty programs and targeted promotions.

---

## Conclusion

This analysis offers a comprehensive view of the retail store's performance, helping stakeholders make data-driven decisions on product offerings, regional marketing, and inventory management. The insights provided in the Power BI dashboard allow for quick and interactive exploration of key sales metrics.

--- 
