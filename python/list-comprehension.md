# Python：列表推导式什么时候该用、什么时候不该

```python
# 好的用法：一行能说清的转换
squares = [x * x for x in range(10) if x % 2 == 0]

# 不好的用法：嵌套两层以上，可读性崩了
bad = [[y for y in row if y > 0] for row in matrix if len(row) > 2]
```

经验：

- 推导式里只做一件事：转换或过滤，二选一。
- 需要副作用（打印、写文件）时用普通循环，推导式不是干这个的。
- 生成器表达式 `(x for x in ...)` 不立即求值，处理大文件时省内存。
