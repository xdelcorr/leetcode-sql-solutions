# Problem

Given a `Person` table, return every email address that appears more than once.

# Approach

The solution groups rows by `email` and counts how many times each value appears. Once the records are grouped, only the emails with a count greater than one are kept. This works because duplicate emails will naturally form groups with multiple rows.

# Key Idea

Use `GROUP BY` on the `email` column and filter the grouped results with `HAVING` so only duplicated email values remain.

# Step-by-Step Explanation

1. Read all rows from the `Person` table.
2. Group the rows by `email` so identical email addresses are collected together.
3. Count how many rows exist in each email group.
4. Keep only the groups where the count is greater than `1`.
5. Return the email values from those groups.

# SQL Query / Code

```sql
SELECT email
FROM Person
GROUP BY email
HAVING COUNT(*) > 1;
```

# Notes

- The `id` column does not affect the result because the task is only concerned with repeated email values.
- The result can be returned in any order.

