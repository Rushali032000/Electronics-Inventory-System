# 📦 Electronic Inventory System (EIS)

A comprehensive inventory management system for an electronics store, managing products, suppliers, orders, promotions, and sales transactions. Built in **PostgreSQL**, this project demonstrates ER modeling, relational schema creation, data manipulation, and advanced SQL query logic.

---

## Contents

- [`DDL.txt`](./DDL.txt): Database schema (table definitions, keys, constraints)
- [`INSERT_statements.txt`](./INSERT_statements.txt): Sample data and updates
- [`SQL Queries.txt`](./SQL%20Queries.txt): Functional SQL queries, views, triggers, and procedures

---

##  Schema Overview

This system manages:

| Table                | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `Supplier`           | Supplier details (name, contact, location, etc.)                            |
| `Product`            | Product info including category, pricing, thresholds, and supplier link     |
| `Purchase_Order`     | Order details with quantity and expected delivery dates                     |
| `Ordered`            | Products included in each purchase order                                    |
| `Storage_Location`   | Aisles and shelves where products are stored                                |
| `ProductInstance`    | Individual product units with color and location                            |
| `Promotions`         | Discount offers based on promo types and dates                              |
| `Has_Promo`          | Relationship between products and their applied promotions                  |
| `Employee`           | Store employees involved in transactions                                    |
| `Sales_Transaction`  | Product sale records with payment and billing info                          |
| `ReturnedProducts`   | Returned units with reasons and refund amounts                              |
| `Damaged_Products`   | Logged damaged units with damage details                                    |

---

## 💾 Features

### ✅ Database Design
- All relations normalized to **BCNF**
- Proper use of **primary & foreign keys**
- Meaningful **constraints** (`NOT NULL`, `UNIQUE`, `DEFAULT`, etc.)
- Referential integrity maintained via `ON DELETE` and `ON UPDATE` actions

### 📊 Data Operations
- Over **100+ `INSERT` statements** for products, orders, transactions, and more
- `ALTER TABLE` used to evolve schema to match real-world demands (e.g., refund amount)

### 🧠 Functional SQL
- ✅ Sales summaries
- ✅ Inventory value calculation
- ✅ Supplier-specific queries
- ✅ Order delay tracking
- ✅ Reorder planning & slow-moving product logic
- ✅ Trigger-based inventory updates

---

## 🔁 Triggers & Stored Procedures

The following advanced features are implemented in `SQL Queries.txt`:

| Feature | Type |
|--------|------|
| Auto-update stock after a sale | `Trigger + Function` |
| Auto-increment stock after return | `Trigger + Function` |
| Auto-update after purchase order delivery | `Trigger + Function` |
| Mark returned product as sold | `Trigger + Function` |
| Flag slow-moving products | `Stored Procedure` |
| Delete discontinued & unsold products | `Stored Procedure` |

---

## 🔍 Sample Queries

```sql
-- Get all products from 'Maple' supplier
SELECT P.ProductID, P.PName, P.SellingPrice
FROM Product P
JOIN Supplier S ON P.SupplierID = S.SupplierID
WHERE S.Sname = 'Maple';

-- Inventory value calculation
CREATE VIEW Inventory_Value AS
SELECT SUM(StockLevel * CostPrice) AS TotalInventoryValue
FROM Product;
