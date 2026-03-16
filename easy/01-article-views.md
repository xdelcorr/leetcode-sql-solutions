# Problem

Given the `Views` table, return the IDs of authors who viewed at least one of their own articles. The result should contain each qualifying author only once and be sorted by `id` in ascending order.

# Approach

The solution checks for rows where the author and viewer are the same person. Those rows represent self-views, which are the only records needed for this problem. Since the table can contain duplicate rows, `DISTINCT` is used to ensure each author appears only once in the final result. The output is then sorted by the required column.

# Key Idea

If `author_id = viewer_id`, the author viewed their own article. Select those authors, remove duplicates, and order the result by `id`.

# Step-by-Step Explanation

1. Read the rows from the `Views` table.
2. Filter the data to keep only the rows where `author_id` matches `viewer_id`.
3. Select the author ID from those matching rows and rename it to `id`.
4. Use `DISTINCT` to avoid returning the same author more than once.
5. Sort the final result in ascending order by `id`.

# SQL Query / Code

```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

# Notes

- Duplicate rows in the table do not affect the final result because `DISTINCT` removes repeated author IDs.
- The query only needs `author_id` and `viewer_id`; the article and date columns are not required for this output.
