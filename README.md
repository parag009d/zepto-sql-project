#  Zepto Product Data Analysis Using SQL



## Overview

This project presents an exploratory and analytical SQL study of Zepto’s product inventory dataset. The goal is to understand product availability, pricing strategies, category performance, and consumer value using SQL queries on cleaned transactional data. The dataset simulates a live product catalog for an online grocery delivery platform. It includes attributes like product names, categories, MRP, discounted price, availability, weight, discount %, and stock levels.

The project is designed to mimic the daily analytical tasks of a data analyst or business intelligence associate in the e-commerce space — focusing on insights extraction, inventory evaluation, and revenue forecasting using SQL only.

---

## Objectives

- Explore and clean the Zepto dataset for better analysis.
- Identify top-value products based on discount and price per gram.
- Analyze out-of-stock products and their pricing strategy.
- Estimate potential revenue across different product categories.
- Group products based on size (Low, Medium, Bulk) and evaluate weight distribution.
  

## Dataset

- **File Used:** `zepto_v2
- .csv`
- **Rows:** ~900 product entries
- **Fields:** SKU ID, category, product name, MRP, discounts, available quantity, out-of-stock status, weight, etc.
- **Data Type:** Structured CSV → Imported to MySQL

---

## Schema

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
## problems and solutions

### 1. Top 10 Best-Value Products Based on Discount Percentage
```sql
SELECT DISTINCT name, mrp, discountPercent
FROM zepto
ORDER BY discountPercent DESC
LIMIT 10;
```
### 2. Products with High MRP but Out of Stock
```sql
SELECT DISTINCT name, mrp
FROM zepto
WHERE outOfStock = TRUE AND mrp > 300
ORDER BY mrp DESC;
```
### 3. Estimated Revenue per Product Category
```sql
SELECT category,
SUM(discountedSellingPrice * availableQuantity) AS total_revenue
FROM zepto
GROUP BY category
ORDER BY total_revenue DESC;
```
### 4. Products with MRP > ₹500 and Discount < 10%
```sql
SELECT DISTINCT name, mrp, discountPercent
FROM zepto
WHERE mrp > 500 AND discountPercent < 10
ORDER BY mrp DESC, discountPercent DESC;
```
### 5. Top 5 Categories by Average Discount Percentage
```sql
SELECT category,
ROUND(AVG(discountPercent), 2) AS avg_discount
FROM zepto
GROUP BY category
ORDER BY avg_discount DESC
LIMIT 5;
```
### 6. Best Price per Gram for Products Above 100g
```sql
SELECT DISTINCT name, weightInGms, discountedSellingPrice,
ROUND(discountedSellingPrice / weightInGms, 2) AS price_per_gram
FROM zepto
WHERE weightInGms >= 100
ORDER BY price_per_gram;
```
### 7. Categorize Products into Low, Medium, Bulk by Weight
```sql
SELECT DISTINCT name, weightInGms,
CASE 
  WHEN weightInGms < 1000 THEN 'Low'
  WHEN weightInGms < 5000 THEN 'Medium'
  ELSE 'Bulk'
END AS weight_category
FROM zepto;
```
### 8. Total Inventory Weight per Category
```sql
SELECT category,
SUM(weightInGms * availableQuantity) AS total_weight
FROM zepto
GROUP BY category
ORDER BY total_weight DESC;
```
##  Conclusion
- Cleaned and prepared a structured e-commerce dataset containing SKU-level details of over 900 grocery products.
- Identified that categories like Beverages and Staples offer the highest total potential revenue based on available quantity and price.
- Discovered that some high-MRP products remain out of stock, potentially signaling demand–supply mismatches or pricing issues.
- Found the best-value products by computing price per gram and discount percentages, useful for pricing strategy optimization.
- Used conditional logic in SQL to group products by weight category, enabling stock planning based on product size.
