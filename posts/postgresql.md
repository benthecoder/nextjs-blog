---
title: 'PostgreSQL snippets'
date: '2022-02-02'
---

### EXTRACT day/month/year

```sql
EXTRACT(MONTH FROM timestamp '2020-11-30') as month
```

### Is value within an array?

```sql
WHERE 'target' = ANY(column_w_array)
```

### Cast string as time interval

```sql
CAST('2 weeks' AS INTERVAL);
```

### Time difference with AGE

```sql
AGE('date1', 'date2')
```

### query values with space

```sql
WHERE column LIKE '% %'
```

### Extract last n characters from string with RIGHT

```sql
SELECT RIGHT('string', 2) AS res;

# res
# ng
```

### slice string with SUBSTRING

```sql
SUBSTRING('string', <position>, <length>) as subset

# ex: SUBSTRING('string', 1, 3) as subset 
# will give **str**
```

### Increase date on date column with INTERVAL

```sql
date_column + INTERVAL '90 days' AS new_date
```

### filter by average

- use subquery

```sql
WHERE
  price < (SELECT AVG(price) FROM wine_region)
```

### What is OVER() ?

- think of it as an inline groupby statement
- you're able to count average over all rows without a group by

```sql
ROUND(AVG(price) OVER(), 2) AS avg_price
```

### What does OVER(PARTITION BY col) do?

- used to partition data and then perform window functions
- without it, the entire result set is a single partition

### GROUP BY vs PARTITION BY

- in partition by, the row-level details are preserved, that means you still have the original rows and plus the aggregated values
- whereas in group by, the original rows are gone, and you're left with the aggregates only

### Other Window Functions

Besides aggregate functions, there are some other important window functions, such as:

- **`ROW_NUMBER()`**. Returns the sequence number of the row in the result set.
- **`RANK()`**. Similar to **`ROW_NUMBER()`**, but can take a column as an argument. The rank order is determined over the value of this column. If two or more rows have the same value in this column, these rows all get the same rank. The next rank will continue from the equivalent number of rows up; for example, if two rows share a rank of 10, the next rank will be 12.
- **`DENSE_RANK()`**. Very similar to RANK(), except it doesn’t have “gaps.” In the previous example, if two rows share a rank of 10, the next rank will be 11.
- **`NTILE`**. Used to calculate quartiles, deciles, or any other percentiles.
- **`LAG`** & **`LEAD`**. Used to pull values from the previous (**`LAG`**) or the following (**`LEAD`**) row.

### What is CROSS JOIN?

- all combinations of two tables
- don't need Key to join

### HAVING vs WHERE

- HAVING is for aggregate conditions (after GROUP BY)
- WHERE is for individual rows
- RULE: use HAVING after GROUP BY and WHERE before.