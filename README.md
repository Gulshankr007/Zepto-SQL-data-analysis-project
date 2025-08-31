# 🛒 Zepto SQL Data Analysis Project

![Zepto Banner](https://github.com/Gulshankr007/Zepto-SQL-data-analysis-project/blob/55efab7fad774a2640eba0726619281d4f7c981f/Zepto%20.png)

---

## 📌 Overview
This is a **real-world Data Analyst SQL project** based on an **e-commerce inventory dataset** scraped from **Zepto** — one of India’s fastest-growing quick-commerce startups.  

The project simulates **end-to-end analyst workflows**, from raw data exploration ➝ cleaning ➝ SQL queries ➝ business-driven insights.  

---

## 🎯 Goals
Using SQL to:
- ✅ Set up a messy, real-world e-commerce database  
- ✅ Perform **Exploratory Data Analysis (EDA)**  
- ✅ Implement **Data Cleaning** for better quality  
- ✅ Derive **business insights** (pricing, stock, revenue)  

---

## 📁 Dataset Overview
- **Source**: Kaggle (scraped from Zepto’s official listings)  
- **Nature**: Simulates real-world e-commerce catalog data with multiple SKUs for the same product (different pack sizes, discounts, etc.).  

**🧾 Columns:**
| Column | Description |
|--------|-------------|
| `sku_id` | Unique identifier (Primary Key) |
| `name` | Product name |
| `category` | Product category (Fruits, Snacks, Beverages, etc.) |
| `mrp` | Maximum Retail Price (₹, converted from paise) |
| `discountPercent` | Discount applied (%) |
| `discountedSellingPrice` | Final selling price (₹) |
| `availableQuantity` | Inventory units available |
| `weightInGms` | Product weight (grams) |
| `outOfStock` | Boolean flag (true/false) |
| `quantity` | Units per package |

---

## 🔧 Workflow

### 1️⃣ Database & Table Creation

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);

```

2️⃣ Data Import

Imported CSV via pgAdmin.

Fixed UTF-8 encoding issues by saving file in CSV UTF-8 format.

Alternative using \copy:
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv' WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');

3️⃣ Data Exploration 🔍

Counted total records
Sampled dataset structure
Checked NULL values
Extracted distinct product categories
Compared in-stock vs out-of-stock products
Identified duplicate SKUs

4️⃣ Data Cleaning 🧹

Removed rows where mrp or discountedSellingPrice = 0
Converted prices from paise ➝ rupees
Ensured consistency in numeric fields

5️⃣ Business Insights 📊

🔝 Top 10 best-value products (highest discount %)
🚫 High-MRP products currently out of stock
💰 Estimated potential revenue by category
💎 Filtered expensive products (MRP > ₹500) with low discount
📉 Ranked top 5 categories with highest average discounts
⚖️ Calculated price per gram to find value-for-money products
📦 Grouped products into Low / Medium / Bulk weight categories
🏋️ Total inventory weight by product category

SELECT category,
       ROUND(AVG(discountPercent),2) AS avg_discount,
       COUNT(*) AS total_products
FROM zepto
GROUP BY category
ORDER BY avg_discount DESC
LIMIT 5;

🚀 Tech Stack

🗄️ PostgreSQL / pgAdmin
🧑‍💻 SQL (CTEs, Window Functions, Aggregates)
📊 Analytics Tools: Power BI / Tableau-ready outputs

📌 Key Learnings

How to handle real-world messy catalog data
Building scalable SQL queries for insights
Translating raw data ➝ business value
