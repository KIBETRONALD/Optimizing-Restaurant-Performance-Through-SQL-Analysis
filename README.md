 Optimizing-Restaurant-Performance-Through-SQL-Analysis

 #Project Overview
The Restaurant Operations Analysis project evaluates sales performance, customer preferences, and pricing strategies using data from the `menu_items` and `order_details` tables. The goal is to generate actionable insights to optimize menu offerings and improve profitability.

---

# Data Source
Dataset from Maven Analytics:

- **menu_items.csv** → menu_item_id, item_name, category, price  
- **order_details.csv** → order_details_id, order_id, order_date, order_time, item_id  

---

#Technology Used
- SQL (Data Analysis & Queries)

---

# Data Cleaning & Preparation
```sql
SELECT * FROM menu_items;

UPDATE menu_items
SET price = ROUND(price, 2);

SELECT * FROM order_details;

ALTER TABLE order_details
ALTER COLUMN order_time TIME(0);
