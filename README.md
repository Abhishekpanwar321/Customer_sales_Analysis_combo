📊 Customer Sales Analysis Dashboard (SQL + Power BI)
🚀 Project Overview

This project focuses on analyzing customer purchasing behavior using SQL Server and visualizing insights through an interactive Power BI Dashboard.

The objective is to uncover business insights related to:

Customer demographics
Sales performance
Product trends
Subscription behavior
Discount impact
🧰 Tech Stack
💾 SQL Server – Data cleaning, transformation & analysis
📊 Power BI – Data visualization & dashboard creation
🐍 (Optional) Python – Data preprocessing
📁 Dataset – Customer sales dataset
📌 Key KPIs (Dashboard Highlights)
👥 Total Customers: 3.9K
💰 Average Purchase: $59.76
⭐ Average Rating: 3.75
📦 Category-wise Sales & Revenue
👤 Age Group Analysis
🔁 Subscription Insights
📷 Dashboard Preview

(Add your screenshot here in GitHub repo)

![Dashboard](dashboard.png)
🧠 Business Questions Solved (SQL Analysis)
1️⃣ Revenue by Gender
SELECT gender AS Gender, 
       SUM(purchase_amount) AS Revenue
FROM customer
GROUP BY gender;

👉 Insight: Compare spending patterns between male and female customers.

2️⃣ High-Value Discount Customers
SELECT *
FROM customer
WHERE discount_applied = 'Yes'
AND purchase_amount >= (
    SELECT AVG(purchase_amount) FROM customer
);

👉 Insight: Identify customers who used discounts but still spent above average.

3️⃣ Top 5 Products by Rating
SELECT TOP 5 item_purchased,
       AVG(review_rating) AS rating
FROM customer
GROUP BY item_purchased
ORDER BY rating DESC;

👉 Insight: Best-performing products based on customer satisfaction.

4️⃣ Shipping Type Analysis
SELECT shipping_type,
       ROUND(AVG(purchase_amount),2) AS avg_revenue
FROM customer
WHERE shipping_type IN ('Standard','Express')
GROUP BY shipping_type;

👉 Insight: Compare spending behavior across shipping preferences.

5️⃣ Subscription Impact on Revenue
SELECT subscription_status,
       COUNT(*) AS total_customers,
       ROUND(AVG(purchase_amount),2) AS avg_spend,
       SUM(purchase_amount) AS total_spend
FROM customer
GROUP BY subscription_status
ORDER BY total_spend DESC;

👉 Insight: Do subscribed users spend more?

6️⃣ Discount Usage by Product
SELECT TOP 5 item_purchased,
ROUND(100.0 * SUM(CASE WHEN discount_applied='Yes' THEN 1 ELSE 0 END)/COUNT(*),2) AS discount_percentage
FROM customer
GROUP BY item_purchased
ORDER BY discount_percentage DESC;

👉 Insight: Products most influenced by discounts.

7️⃣ Customer Segmentation
WITH customer_type AS (
SELECT customer_id,
CASE 
    WHEN previous_purchases = 1 THEN 'New'
    WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
    ELSE 'Loyal'
END AS customer_segment
FROM customer
)
SELECT customer_segment, COUNT(*) AS total_customers
FROM customer_type
GROUP BY customer_segment;

👉 Insight: Segment customers into New, Returning, and Loyal.

8️⃣ Top Products per Category
WITH item_counts AS (
SELECT category, item_purchased,
COUNT(customer_id) AS total_orders,
ROW_NUMBER() OVER (PARTITION BY category ORDER BY COUNT(customer_id) DESC) AS rank
FROM customer
GROUP BY category, item_purchased
)
SELECT *
FROM item_counts
WHERE rank <= 3;

👉 Insight: Identify best-selling products in each category.

9️⃣ Repeat Buyers vs Subscription
SELECT subscription_status,
COUNT(customer_id) AS repeat_buyers
FROM customer
WHERE previous_purchases > 5
GROUP BY subscription_status;

👉 Insight: Are repeat customers more likely to subscribe?

🔟 Revenue by Age Group
SELECT age_group,
SUM(purchase_amount) AS total_revenue
FROM customer
GROUP BY age_group
ORDER BY total_revenue DESC;

👉 Insight: Which age group contributes most to revenue?

📊 Key Insights
👕 Clothing category generates the highest revenue and sales
👥 Young Adults contribute the most revenue
🚚 Express shipping users spend slightly more than standard users
🎯 Discounts significantly influence product purchases
🔁 Majority customers are loyal (repeat buyers)
📉 Non-subscribers contribute more total revenue (due to higher count)
📈 Power BI Features
Interactive Filters:
Gender
Category
Shipping Type
Subscription Status
Visualizations:
Bar Charts (Sales & Revenue)
Donut Chart (Subscription Split)
KPI Cards
Category Analysis

🎯 Conclusion

This project demonstrates how SQL + Power BI can be used together to:

Extract meaningful insights from raw data
Support business decision-making
Build interactive and professional dashboards
