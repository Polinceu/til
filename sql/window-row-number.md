# SQL：窗口函数 ROW_NUMBER()，TopN 问题终结者

## 需求：每个用户最新的一笔订单

```sql
SELECT *
FROM (
  SELECT o.*,
         ROW_NUMBER() OVER (
           PARTITION BY user_id      -- 按用户分组
           ORDER BY created_at DESC  -- 组内按时间倒序
         ) AS rn
  FROM orders o
) t
WHERE rn = 1;
```

不用 GROUP BY，不用自连接，一遍搞定。

## ROW_NUMBER vs RANK vs DENSE_RANK

```sql
-- 分数都是 100, 100, 90
ROW_NUMBER()  -- 1, 2, 3（不管并列，硬编号）
RANK()        -- 1, 1, 3（并列占名次）
DENSE_RANK()  -- 1, 1, 2（并列不占名次）
```

"取前 3 名（含并列）"用 DENSE_RANK，
"每人只取一条"用 ROW_NUMBER。

## 经典：去重保留最新

```sql
DELETE FROM orders
WHERE id IN (
  SELECT id FROM (
    SELECT id, ROW_NUMBER() OVER (
      PARTITION BY order_no ORDER BY updated_at DESC
    ) AS rn FROM orders
  ) t WHERE rn > 1
);
```

MySQL 8.0+、PostgreSQL 都支持窗口函数，
还在用"GROUP BY + MAX + 回表"的可以换写法了。
