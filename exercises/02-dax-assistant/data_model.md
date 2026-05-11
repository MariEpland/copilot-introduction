# Data Model — Sales Reporting

This document describes the Power BI data model used in Exercise 02.
Three tables, matching the `data/sales_sample.csv` source file.

---

## Tables

### Orders
The fact table. One row per order line.

| Column | Type | Description |
|--------|------|-------------|
| order_id | Text | Unique order identifier (e.g. `ORD0001`) |
| customer_id | Text | FK → Customers |
| product | Text | FK → Products (product name) |
| category | Text | Product category |
| quantity | Whole Number | Units ordered |
| unit_price | Decimal | Price per unit (NOK) |
| order_date | Date | Date of the order |
| region | Text | Sales region (North, South, East, West, Central) |

### Customers
Dimension table. One row per customer.

| Column | Type | Description |
|--------|------|-------------|
| customer_id | Text | Unique customer identifier |
| customer_name | Text | Full name |
| region | Text | Customer's region |

### Products
Dimension table. One row per product.

| Column | Type | Description |
|--------|------|-------------|
| product | Text | Product name (matches Orders[product]) |
| category | Text | Product category |
| unit_price | Decimal | Standard price per unit |

---

## Relationships

```
Customers[customer_id]  →  Orders[customer_id]   (1:many, active)
Products[product]       →  Orders[product]        (1:many, active)
```

---

## Key Measures to Build

| Measure Name | Description |
|-------------|-------------|
| Total Revenue | Sum of quantity × unit_price across all orders |
| North Revenue | Total Revenue filtered to the North region |
| YTD Revenue | Running total revenue from the start of the year |
| Product Revenue Rank | Rank of each product by its total revenue |
| Avg Order Value | Revenue divided by number of orders (safe division) |
