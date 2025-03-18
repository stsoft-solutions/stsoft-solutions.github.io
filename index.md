---
title: Welcome to my blog
---

```sql
WITH stat AS (
  SELECT
    account_balance,
    ROW_NUMBER() OVER (ORDER BY account_balance) AS rn,
    COUNT(*) OVER () AS total_count
  FROM stat_total
)
SELECT FORMAT(AVG(account_balance), 'N0') AS median_account_balance
FROM stat
WHERE rn IN (
  FLOOR((total_count + 1) / 2),
  CEIL((total_count + 1) / 2)
);
```
