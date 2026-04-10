# Data Cleaning & Preparation
```sql
SELECT * FROM menu_items;

UPDATE menu_items
SET price = ROUND(price, 2);

SELECT * FROM order_details;

ALTER TABLE order_details
ALTER COLUMN order_time TIME(0);

Objectives
Explore the menu_items table
Explore the order_details table
Analyze how customers respond to the new menu
 Business Needs Addressed
Menu Optimization: Identify underperforming items
Pricing Strategy Improvement: Evaluate price vs demand
Sales Growth: Increase order value and frequency
Customer Retention: Improve repeat purchases
 Methodology
Data exploration using SQL
Aggregation and grouping
Table joins for deeper insights
KPI-driven analysis
s
i).Menu Items Analysis

1.Total Items on Menu

SELECT COUNT(*) FROM menu_items;

= 32 items

2.Pricing Analysis

SELECT * FROM menu_items ORDER BY price;
SELECT * FROM menu_items ORDER BY price DESC;

. Least expensive: Edamame ($5.00)
. Most expensive: Shrimp Scampi ($19.95)

3.Italian Dishes

SELECT COUNT(*) FROM menu_items WHERE category = 'Italian';

= 9 dishes

SELECT * FROM menu_items WHERE category = 'Italian' ORDER BY price;

.Least expensive: Spaghetti ($14.50)

SELECT * FROM menu_items WHERE category = 'Italian' ORDER BY price DESC;

. Most expensive: Shrimp Scampi ($19.95)

3.Category Distribution

SELECT category, COUNT(menu_item_id)
FROM menu_items
GROUP BY category;

= American: 6 | Asian: 8 | Italian: 9 | Mexican: 9

4.Average Price by Category

SELECT category, AVG(price)
FROM menu_items
GROUP BY category;

= Italian: $16.75 (highest)
= American: $10.07 (lowest)

ii) Order Details Analysis

Date Range

SELECT MIN(order_date), MAX(order_date)
FROM order_details;

1) Jan 01, 2023 – Mar 31, 2023

Total Orders

2)SELECT COUNT(DISTINCT order_id) FROM order_details;

= 5,370 orders

3.Total Items Ordered

SELECT COUNT(*) FROM order_details;

= 12,234 items

3.Orders with Most Items

SELECT order_id, COUNT(item_id)
FROM order_details
GROUP BY order_id
ORDER BY COUNT(item_id) DESC;

= Max items: 14

4.Orders with More Than 12 Items

SELECT COUNT(*)
FROM (
  SELECT order_id
  FROM order_details
  GROUP BY order_id
  HAVING COUNT(item_id) > 12
) AS num_orders;

= 20 orders

III) Customer Behavior Analysis (Joined Tables)

Join Tables

SELECT *
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id;

1)Most & Least Ordered Items

SELECT item_name, COUNT(*) AS num_orders
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
GROUP BY item_name
ORDER BY num_orders DESC;

=Most ordered: Hamburger (622)
= Least ordered: Chicken Tacos (123)

2.Top 5 Highest-Spending Orders

SELECT TOP 5 order_id, SUM(price) AS total_spend
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
GROUP BY order_id
ORDER BY total_spend DESC;

= Highest: $192.15 (Order #440)

3.Highest Spending Order Breakdown

SELECT category, COUNT(item_id)
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
WHERE order_id = 440
GROUP BY category;

= Italian dominates (8 items)

4.Top Orders Category Insights

SELECT category, COUNT(item_id)
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id
WHERE order_id IN (440, 2075, 1957, 330, 2675)
GROUP BY category;

= Italian: 26 items | American: 10 items

Key Insights

I)Menu & Pricing

Italian dishes are the most expensive ($16.75 avg)
American dishes are the cheapest ($10.07 avg)
Balanced menu across categories
Price range: $5.00 – $19.95

II)Customer Behavior

5,370 orders and 12,234 items in 3 months
Italian dominates high-value orders
Hamburger is the most popular item
American drives volume but not high revenue

III)Order Patterns

Most orders are moderate
20 large orders (>12 items)
Highest order: $192.15
High spenders prefer Italian
 Recommendations

Menu Optimization

Improve or replace Chicken Tacos

Pricing Strategy

Increase price of high-demand items (e.g., Hamburger)

Revenue Growth

Introduce premium American dishes
Promote high-margin items

Customer Strategy

Create Italian combo deals
Launch loyalty program for high spenders

Operational Efficiency

Optimize staffing during peak hours
Improve preparation efficiency for popular dishes



