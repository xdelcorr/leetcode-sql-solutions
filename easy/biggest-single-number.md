# Biggest Single Number

# Problem

Given the `MyNumbers` table, find the largest value that appears exactly once. If no number appears only one time, return `NULL`.

# Approach

The solution identifies which numbers occur only once and then selects the largest value from that filtered set. This works because the problem is not asking for the largest number overall, but specifically the largest number whose frequency is exactly one.

To do that, the query groups rows by `num`, counts how many times each number appears, keeps only the groups with a count of `1`, and then returns the maximum value among those remaining numbers.

# Key Idea

Treat each distinct number as a group, filter for groups that appear once, and then take the largest value from those valid groups.

# Step-by-Step Explanation

1. Read all values from `MyNumbers`.
2. Group the rows by `num` so each distinct number is evaluated once.
3. Count how many rows belong to each grouped number.
4. Keep only the numbers whose count is exactly `1`.
5. Return the largest number from that filtered result.
6. If no grouped number meets the condition, the result is `NULL`.

# SQL Query / Code

```sql
SELECT MAX(num) AS num
FROM (
    SELECT num
    FROM MyNumbers
    GROUP BY num
    HAVING COUNT(num) = 1
) AS single_numbers;
```

# Notes

- The result should be a single value representing the largest valid single number.
- If every number appears more than once, returning `NULL` satisfies the problem requirement.
