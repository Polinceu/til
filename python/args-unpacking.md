# Python：*args / **kwargs 与解包调用

函数参数前面的星号一直半懂不懂，今天彻底搞明白了。

## 定义时：收集多余参数

```python
def f(a, *args, **kwargs):
    print("a =", a)
    print("args =", args)      # 元组
    print("kwargs =", kwargs)  # 字典

f(1, 2, 3, x=4, y=5)
# a = 1
# args = (2, 3)
# kwargs = {'x': 4, 'y': 5}
```

## 调用时：拆开再传

```python
nums = [1, 2, 3]
print(*nums)          # 等价于 print(1, 2, 3)

opts = {"sep": "-", "end": "!"}
print("a", "b", **opts)  # 等价于 print("a", "b", sep="-", end="!")
```

## 实际用处：写装饰器/转发参数

```python
def log_call(fn):
    def wrapper(*args, **kwargs):
        print(f"calling {fn.__name__}")
        return fn(*args, **kwargs)
    return wrapper
```

记住一句话就行：**定义时是"收"，调用时是"拆"**。
