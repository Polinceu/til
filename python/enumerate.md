# Python：enumerate 不只是"带下标的 for"

```python
fruits = ["apple", "banana", "cherry"]

# 基础：下标从 0 开始
for i, f in enumerate(fruits):
    print(i, f)

# start 参数：下标从 1 开始，适合行号
for n, line in enumerate(open("a.txt"), start=1):
    print(n, line.rstrip())

# 配合条件找下标
names = ["a", "b", "c"]
idx = next(i for i, n in enumerate(names) if n == "b")
print(idx)  # 1
```

- 需要下标时用 `enumerate`，别再写 `for i in range(len(x))`。
- `start` 参数能省掉 `i + 1` 这种小算术。
- `next` + 生成器找第一个满足条件的下标，比 `list.index` 灵活。
