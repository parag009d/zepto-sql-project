#  Zepto Product Data Analysis Using SQL

![Zepto Banner](https://cdn.zeptonow.com/zepto-logo-light.png)

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
- Practice case-based, industry-relevant SQL problem solving.

---

## Dataset

The dataset was structured to resemble Zepto’s live product catalog, reflecting essential e-commerce product metrics:

- **File Used:** `zepto_v2.csv`
- **Rows:** ~900 product entries
- **Fields:** SKU ID, category, product name, MRP, discounts, available quantity, out-of-stock status, weight, etc.
- **Data Type:** Structured CSV → Imported to PostgreSQL/MySQL

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
