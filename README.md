# 📊 Sales Data Analysis using SQL

This project showcases the power of SQL for performing business data analysis. The dataset used simulates retail sales and contains information about product types, sales, outlet characteristics, and customer feedback ratings. Through structured queries and data cleaning techniques, we derive actionable insights and key performance indicators (KPIs) for business decision-making.

---

## 🛠️ Technologies Used

* **SQL** (Structured Query Language)
* **Relational Database Management System** (PostgreSQL)
* **Data Cleaning & Transformation**
* **Analytical Querying & KPI Reporting**

---

## 🧹 Data Cleaning

To ensure accuracy and consistency, we standardized the `Item_Fat_Content` column:

```sql
UPDATE sales_data
SET Item_Fat_Content = 
    CASE 
        WHEN Item_Fat_Content IN ('LF', 'low fat') THEN 'Low Fat'
        WHEN Item_Fat_Content = 'reg' THEN 'Regular'
        ELSE Item_Fat_Content
    END;
```

✔️ **Why?**
Inconsistent labeling (like `LF`, `low fat`, `reg`) can result in incorrect aggregations and insights. This standardization helps maintain data quality and uniformity.

---

## 📌 Key Performance Indicators (KPIs)

### 🔢 A. Sales Metrics

| Metric           | Description                | SQL Function Used |
| ---------------- | -------------------------- | ----------------- |
| `Total Sales`    | Overall sales in million   | `SUM()`           |
| `Average Sales`  | Average revenue per entry  | `AVG()`           |
| `No. of Items`   | Total items/orders counted | `COUNT()`         |
| `Average Rating` | Average customer rating    | `AVG()`           |

```sql
SELECT CAST(SUM(Total_Sales) / 1000000.0 AS DECIMAL(10,2)) AS Total_Sales_Million FROM sales_data;
SELECT CAST(AVG(Total_Sales) AS INT) AS Avg_Sales FROM sales_data;
SELECT COUNT(*) AS No_of_Orders FROM sales_data;
SELECT CAST(AVG(Rating) AS DECIMAL(10,1)) AS Avg_Rating FROM sales_data;
```

---

## 📂 Grouped Analysis

### 🍔 B. Total Sales by Fat Content

```sql
SELECT Item_Fat_Content, SUM(Total_Sales) AS Total_Sales
FROM sales_data
GROUP BY Item_Fat_Content;
```

### 🛍️ C. Total Sales by Item Type

```sql
SELECT Item_Type, SUM(Total_Sales) AS Total_Sales
FROM sales_data
GROUP BY Item_Type
ORDER BY Total_Sales DESC;
```

### 🏢 E. Sales by Outlet Establishment Year

```sql
SELECT Outlet_Establishment_Year, SUM(Total_Sales) AS Total_Sales
FROM sales_data
GROUP BY Outlet_Establishment_Year
ORDER BY Outlet_Establishment_Year;
```

---

### 🏪 F. Percentage of Sales by Outlet Size

```sql
SELECT 
    Outlet_Size, 
    SUM(Total_Sales) AS Total_Sales,
    CAST((SUM(Total_Sales) * 100.0 / SUM(SUM(Total_Sales)) OVER()) AS DECIMAL(10,2)) AS Sales_Percentage
FROM sales_data
GROUP BY Outlet_Size
ORDER BY Total_Sales DESC;
```

### 🌍 G. Sales by Outlet Location

```sql
SELECT Outlet_Location_Type, SUM(Total_Sales) AS Total_Sales
FROM sales_data
GROUP BY Outlet_Location_Type
ORDER BY Total_Sales DESC;
```

---

## 📊 H. All Metrics by Outlet Type

```sql
SELECT Outlet_Type, 
    SUM(Total_Sales) AS Total_Sales,
    AVG(Total_Sales) AS Avg_Sales,
    COUNT(*) AS No_Of_Items,
    AVG(Rating) AS Avg_Rating,
    AVG(Item_Visibility) AS Item_Visibility
FROM sales_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;
```

---

## 🎯 Insights & Learnings

* Standardizing data values ensures more accurate grouping and reporting.
* SQL is a powerful tool for extracting business insights from raw datasets.
* Understanding customer and outlet behaviors via data segmentation helps drive targeted strategies.

---


## 📁 Dataset Info

 fields include:

* `Item_Type`, `Item_Fat_Content`, `Item_Visibility`, `Total_Sales`, `Rating`
* `Outlet_Size`, `Outlet_Type`, `Outlet_Location_Type`, `Outlet_Establishment_Year`

---

## 🧠 Author

**Sunil Ping**
Sales, Business Development, & Data Analysis Enthusiast


---

## 💬 Feedback

Have suggestions? Want to collaborate on data analytics or SQL projects? Feel free to connect!

