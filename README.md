# LITA-CAPSTONE-PROJECT-SALES-DATA-
# Sales Performance Analysis for a Retail Store

TABLE OF CONTENTS

[Project Overview](#project-overview)

[Project Summary](#project-summary)

[Project Structure](#project-structure)

[SQL Analysis](#sql-analysis)

[Power BI Dashboard](#power-bi-dashboard)

[Key Insights](#key-insights)


### Project Overview
This project involves analyzing the sales performance of a retail store to uncover valuable insights. The analysis spans three primary tools—Excel, SQL, and Power BI—and focuses on identifying trends in product sales, regional performance, and monthly sales, with the final output visualized in an interactive Power BI dashboard.

---

## Project Summary

- **Objective**: To analyze sales data for a retail store, identify top-selling products, examine regional and monthly trends, and provide actionable insights.
- **Tools Used**: Microsoft Excel, SQL Server, Power BI
- **Outcome**: An interactive Power BI dashboard that visualizes the sales trends, top products, and regional performance.

---

## Project Structure

1. **Excel Analysis**: [Download Here](https://drive.google.com/file/d/1y1eAeoNXLUbWVF76y5wo9XMWiC8oj1UO/view?usp=sharing)
   - **Initial Exploration**: Explored sales data using pivot tables for summarizing total sales by product, region, and month.
   - **Metric Calculations**:
     - Calculated average sales per product and total revenue by region.
     - Additional report generated for overall performance by different criteria (e.g., product and month).
     

2. **SQL Analysis**:
   - **Dataset Loading**: Loaded the dataset into SQL Server for deeper analysis.
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
   

3. **Power BI Dashboard**:
   - **Overview**: Created an interactive dashboard summarizing key insights.
   - **Visualizations**:
     - **Sales Overview**: Displays total sales, average sales, and monthly trend analysis.
     - **Top Products**: Highlights best-selling products by total revenue.
     - **Regional Breakdown**: Visualizes sales contribution by each region and top-performing regions.
     - 
   - **Preview**: ![add powerbi image here] 

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
