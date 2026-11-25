# SQL：WHERE 条件的几个细节

```sql
-- 范围：BETWEEN 包含两端
SELECT * FROM orders WHERE amount BETWEEN 100 AND 200;

-- 多个值：IN 比一堆 OR 清楚
SELECT * FROM users WHERE status IN ('active', 'pending');

-- 模糊：LIKE，% 任意多个字符，_ 一个字符
SELECT * FROM users WHERE name LIKE '张%';

-- 空值：必须用 IS NULL，= NULL 永远是假
SELECT * FROM users WHERE email IS NULL;
```

- `BETWEEN` 包含两端，`BETWEEN 100 AND 200` 就是 `>= 100 AND <= 200`。
- `= NULL` 永远不成立，查空值必须用 `IS NULL` / `IS NOT NULL`。
- `IN` 列表别太长，几千个值时考虑先放临时表再 JOIN。
