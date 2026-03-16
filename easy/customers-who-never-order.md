# Problem

Find the names of customers who do not have any matching record in the `Orders` table.

# Approach

The solution treats `Customers` as the main table because every customer must be checked, whether they have placed an order or not. It then compares each customer against the `Orders` table using the customer ID.

By applying a `LEFT JOIN`, all customers remain in the result set. If a customer has never placed an order, the joined row from `Orders` is missing, which appears as `NULL`. Filtering for those `NULL` matches isolates only the customers who never ordered anything.

# Key Idea

Use a `LEFT JOIN` from `Customers` to `Orders`, then keep only the rows where no matching order exists.

# Step-by-Step Explanation

1. Start with the `Customers` table so every customer is included in the comparison.
2. Join the `Orders` table on `Customers.id = Orders.customerId`.
3. Use a `LEFT JOIN` so customers without orders are still returned.
4. Check the joined `Orders` columns for `NULL` values, which indicate no matching order was found.
5. Return the customer name with the required alias.

# SQL Query / Code

```sql
SELECT c.name AS Customers
FROM Customers AS c
LEFT JOIN Orders AS o
    ON c.id = o.customerId
WHERE o.id IS NULL;
```

# Notes

- The result can be returned in any order.
- Customers with one or more matching orders are excluded because their joined `Orders` row is not `NULL`.
