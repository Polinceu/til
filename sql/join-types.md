# SQL：JOIN 类型图解（文字版）

假设 `users(id, name)`，`orders(id, user_id, amount)`。

## INNER JOIN：只取交集

```sql
SELECT u.name, o.amount
FROM users u
INNER JOIN orders o ON o.user_id = u.id;
```

没下过单的用户不出现，没用户的订单也不出现。

## LEFT JOIN：左表全要

```sql
SELECT u.name, o.amount
FROM users u
LEFT JOIN orders o ON o.user_id = u.id;
```

用户全出来，没订单的 amount 是 NULL。
查"没下过单的用户"：

```sql
SELECT u.name FROM users u
LEFT JOIN orders o ON o.user_id = u.id
WHERE o.id IS NULL;
```

## RIGHT JOIN / FULL JOIN

- RIGHT：右表全要，和 LEFT 镜像。
- FULL：两边全要，MySQL 不支持，用 UNION 拼。

## 坑

1. ON 里写错关联字段，结果集爆炸（笛卡尔积）。
2. 一对多 JOIN 后再 COUNT，记得 `COUNT(DISTINCT ...)`。
3. 先想"我要哪边全保留"，再选 LEFT 还是 INNER，
   别上来就 INNER，发现数据少了再改。
