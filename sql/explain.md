# SQL：EXPLAIN，慢查询先看它再动手

查询慢了别先加索引，`EXPLAIN` 看一眼执行计划，多数时候一眼就能看出问题。

```sql
EXPLAIN SELECT * FROM orders WHERE user_id = 123 AND status = 'paid';
```

## 重点看三列（MySQL）

- `type`：访问方式，从好到坏大概是 `const` > `ref` > `range` > `index` > `ALL`。
  看到 `ALL` 就是全表扫描，先怀疑它。
- `key`：实际用到的索引，`NULL` 表示一个都没用上。
- `rows`：预估要扫描的行数，越大越可疑。

## Extra 里的信号

- `Using filesort`：要额外排序，考虑给排序字段加索引。
- `Using temporary`：用了临时表，`GROUP BY` / `DISTINCT` 时常见。
- `Using index`：好消息，覆盖索引，不用回表。

## 习惯

- 改索引前后都跑一次 `EXPLAIN` 对比，别凭感觉。
- `EXPLAIN` 的 `rows` 是估算值，数据量小的时候不准，结合慢查询日志一起看。
