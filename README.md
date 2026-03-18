#  Grocery Store Management — SQL Project

![MySQL](https://img.shields.io/badge/MySQL-8.0-blue?logo=mysql&logoColor=white)
![SQL](https://img.shields.io/badge/Language-SQL-orange)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

A fully normalized MySQL relational database simulating the backend of a grocery store. The project covers end-to-end database design — schema creation, data relationships, and 25+ business analytics queries across 6 domains.

---

## Project Structure

```
Grocery-Store-Management/
│
├── Grocery_Store_Management.sql   # Full schema + all analytical queries
└── README.md
```

---

## Database Schema

The database `GSM` contains **7 interrelated tables** with referential integrity enforced via foreign keys (`ON UPDATE CASCADE`, `ON DELETE CASCADE`).

| Table | Description |
|---|---|
| `supplier` | Vendor details — ID, name, address |
| `categories` | Product category list |
| `employees` | Staff records — ID, name, hire date |
| `customers` | Customer profiles — ID, name, address |
| `products` | Product catalog linked to supplier & category |
| `orders` | Order headers linked to customer & employee |
| `order_details` | Line items with quantity, unit price & total |

### Entity Relationship Overview

```
supplier ──< products >── categories
                │
            order_details
                │
customers ──< orders >── employees
```

---

##  Analytics Performed

### 1. Customer Insights
- Count of unique customers who placed orders
- Customers ranked by order frequency
- Total and average purchase value per customer
- Top 5 customers by lifetime spend

### 2. Product Performance
- Product count and average price by category
- Highest-selling products by quantity sold
- Total revenue generated per product
- Cross-dimensional sales breakdown: category × supplier

### 3. Sales & Order Trends
- Total order count and average order value
- Dates with peak order activity
- Monthly order volume and revenue trends
- Weekday vs. weekend order pattern analysis

### 4. Supplier Contribution
- Total number of suppliers
- Supplier with the highest product count
- Average product price per supplier
- Suppliers ranked by total revenue contribution

### 5. Employee Performance
- Number of active employees who processed orders
- Employees ranked by orders handled
- Total sales value processed per employee
- Average order value handled per employee

### 6. Order Details Deep Dive
- Relationship between quantity ordered and total price
- Average quantity ordered per product
- Unit price variation across products and orders

---

##  Tech Stack

| Tool | Usage |
|---|---|
| MySQL 8.0 | Database engine |
| MySQL Workbench | Query development & execution |
| SQL (DDL + DML) | Schema creation and analytics |

---

##  How to Run

**Prerequisites:** MySQL 8.0+ installed (or MySQL Workbench)

```sql
-- Step 1: Open MySQL Workbench or your MySQL CLI

-- Step 2: Run the full script
source Grocery_Store_Management.sql;

-- Step 3: Verify tables were created
USE GSM;
SHOW TABLES;

-- Step 4: Populate tables with sample data, then run any analytical query
```

---

##  Key SQL Techniques Used

- **Multi-table JOINs** — INNER JOIN across 3–4 tables simultaneously
- **Aggregate functions** — `SUM`, `AVG`, `COUNT`, `MAX`
- **Subqueries & derived tables** — nested SELECT for per-order calculations
- **Date functions** — `STR_TO_DATE`, `DAYOFWEEK`, `LEFT(date, 7)` for month extraction
- **Filtering & ranking** — `GROUP BY`, `ORDER BY`, `LIMIT`, `HAVING`
- **Schema design** — Primary keys, foreign keys, `AUTO_INCREMENT`, `DECIMAL` precision
- **Referential integrity** — `ON UPDATE CASCADE` / `ON DELETE CASCADE`

---

##  Sample Query — Monthly Revenue Trend

```sql
SELECT
    LEFT(o.order_date, 7)          AS order_month,
    COUNT(DISTINCT o.ord_id)       AS order_volume,
    SUM(od.quantity * od.each_price) AS total_revenue
FROM orders o
JOIN order_details od ON o.ord_id = od.ord_id
GROUP BY order_month
ORDER BY order_month;
```

---

##  Potential Improvements

- Store `order_date` as `DATE` type instead of `VARCHAR` for proper indexing
- Add indexes on foreign key columns for query performance
- Introduce an `inventory` table for stock-level tracking
- Add a `returns` table for refund and return analysis
- Create SQL `VIEWS` for frequently used analytics
- Use stored procedures to encapsulate report generation

---

##  Author
saikiran reddy
[saikiranr717@gmail.com](url)
[linkedin.com/in/saikiran-r717](url)

feel free to DM

**[Your Name]**
📧 your.email@example.com
🔗 [LinkedIn](https://linkedin.com) | [GitHub](https://github.com)

---

> ⭐ If you found this project useful, feel free to star the repo!
