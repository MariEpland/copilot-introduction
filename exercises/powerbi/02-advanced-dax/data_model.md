# Data Model Reference

This document describes the semantic model structure for the Power BI exercises.

---

## sales_sample Table

The main fact table containing sales transaction data.

### Columns

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| `order_id` | Text | Unique identifier for each order |
| `customer_id` | Text | Unique identifier for each customer |
| `customer_name` | Text | Customer's full name |
| `product` | Text | Product name |
| `category` | Text | Product category |
| `quantity` | Whole Number | Number of units sold |
| `unit_price` | **Text** | Price per unit (**stored as text, use VALUE() to convert**) |
| `order_date` | Date | Date the order was placed |
| `region` | Text | Geographic region (e.g., "North", "South", "East", "West") |

### Important Notes

⚠️ **unit_price is stored as TEXT**, not as a number. When calculating revenue, you must use `VALUE(sales_sample[unit_price])` to convert it to a numeric value.

### Sample Data

```
order_id: ORD001
customer_id: CUST123
customer_name: John Smith
product: Laptop
category: Electronics
quantity: 2
unit_price: "899.99"
order_date: 2024-01-15
region: North
```

### Relationships

- **Date Table**: The `order_date` column has an auto-generated relationship to a local date table (`LocalDateTable_*`) for time intelligence functions.

---

## Common DAX Patterns for this Model

### Calculate Total Revenue
```dax
SUMX(
    sales_sample,
    sales_sample[quantity] * VALUE(sales_sample[unit_price])
)
```

### Filter by Region
```dax
CALCULATE(
    [Total Revenue],
    sales_sample[region] = "North"
)
```

### Time Intelligence
```dax
TOTALYTD([Total Revenue], sales_sample[order_date])
```

### Ranking
```dax
RANKX(
    ALL(sales_sample[product]),
    [Total Revenue],
    ,
    DESC
)
```

---

## Tips for Copilot

When asking Copilot to write DAX measures for this model:

1. **Always mention** that `unit_price` is stored as text and needs `VALUE()` conversion
2. **Specify the table name** `sales_sample` in your prompts
3. **Reference this file** in your prompts: *"Using the sales_sample table described in data_model.md..."*
4. **Be specific about the business requirement** rather than just asking for DAX code
