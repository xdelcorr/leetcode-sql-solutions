# Combining Two Tables

# Problem

Retrieve each person's first name and last name from the `Person` table, along with their city and state from the `Address` table. If a person does not have a matching address record, the address fields should appear as `NULL`.

# Approach

The solution starts with the `Person` table because every person must be included in the final result. It then joins `Address` on `personId` so address details are added when a matching record exists.

A `LEFT JOIN` is the correct choice because it preserves all rows from `Person`, even when there is no related row in `Address`. This matches the requirement to return every person and show `NULL` for missing address information.

# Key Idea

Use a `LEFT JOIN` from `Person` to `Address` so that all people remain in the result set while address columns are filled only when a matching `personId` exists.

# Step-by-Step Explanation

1. Select the required output columns: first name, last name, city, and state.
2. Use `Person` as the base table to ensure every person is included.
3. Join `Address` using the shared `personId` column.
4. Apply a `LEFT JOIN` so unmatched people are still returned.
5. When no address is found, SQL automatically returns `NULL` for `city` and `state`.

# SQL Query / Code

```sql
SELECT
    p.firstName,
    p.lastName,
    a.city,
    a.state
FROM Person AS p
LEFT JOIN Address AS a
    ON p.personId = a.personId;
```

# Notes

- An `INNER JOIN` would exclude people without an address, which would not satisfy the problem requirements.
- The result can be returned in any order unless additional sorting is explicitly requested.
