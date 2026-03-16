# Combining Two Tables

## Problem

### `Person`

| Column Name | Type    |
| ----------- | ------- |
| personId    | int     |
| lastName    | varchar |
| firstName   | varchar |

personId is the primary key (column with unique values) for this table.
This table contains information about the ID of some persons and their first and last names.

### `Address`

| Column Name | Type    |
| ----------- | ------- |
| addressId   | int     |
| personId    | int     |
| city        | varchar |
| state       | varchar |

addressId is the primary key (column with unique values) for this table.
Each row of this table contains information about the city and state of one person with ID = PersonId.

Write a solution to report the first name, last name, city, and state of each person in the `Person` table. If the address of a `personId` is not present in the `Address` table, report `null` instead.

Return the result table in **any order**.



### Explanation

There is no address in the address table for the personId = 1 so we return null in their city and state.
addressId = 1 contains information about the address of personId = 2.

## SQL Solution

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

## Analysis

This query starts from the `Person` table because the result must include every person, even when no matching address exists.

The `LEFT JOIN` keeps all rows from `Person` and matches rows from `Address` using `personId`. When no matching address is found, `a.city` and `a.state` return `NULL`, which is exactly what the problem asks for.

The selected columns match the required output:

- `p.firstName`
- `p.lastName`
- `a.city`
- `a.state`

### Why `LEFT JOIN` is required

An `INNER JOIN` would remove people who do not have an address record. In the example, `personId = 1` would be excluded, which would be incorrect.
