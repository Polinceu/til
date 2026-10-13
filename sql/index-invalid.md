# SQL：索引失效的几个经典场景

有索引但没走，先怀疑这几个。

## 1. 对索引列用函数/运算

```sql
-- 失效：YEAR() 包住了列
SELECT * FROM orders WHERE YEAR(created_at) = 2026;
-- 改写：范围查询，走索引
SELECT * FROM orders
WHERE created_at >= '2026-01-01' AND created_at < '2027-01-01';
```

## 2. 隐式类型转换

```sql
-- phone 是 varchar，传数字 13800001111
SELECT * FROM users WHERE phone = 13800001111;  -- 失效！
SELECT * FROM users WHERE phone = '13800001111'; -- 走索引
```

MySQL 会把列转成数字再比，索引直接废掉。

## 3. OR 连接非索引列

```sql
SELECT * FROM users WHERE name = 'a' OR age = 20;
-- age 没索引，整个查询全表扫描
```

## 4. LIKE 前导通配符

```sql
WHERE name LIKE '%abc';   -- 失效
WHERE name LIKE 'abc%';   -- 走索引（前缀匹配）
```

## 怎么确认

```sql
EXPLAIN SELECT * FROM users WHERE phone = '13800001111';
```

看 `key` 列有没有值、`type` 是不是 ALL。
ALL = 全表扫描，赶紧优化。
