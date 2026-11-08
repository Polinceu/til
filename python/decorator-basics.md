# Python：装饰器到底在包什么

装饰器就是一个接受函数、返回新函数的函数。`@timer` 这种写法只是语法糖：

```python
import time
import functools

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"{func.__name__} 耗时 {time.time() - start:.3f}s")
        return result
    return wrapper

@timer
def slow():
    time.sleep(0.1)
```

要点：

- 不加 `@functools.wraps`，新函数的 `__name__` 会变成 `wrapper`，调试和文档都受影响。
- 带参数的装饰器要再包一层：外层收参数，内层收函数。
- 装饰器在定义时就执行，不是调用时才执行。
