# Python：raise from 和 bare raise 的区别

```python
try:
    data = open("config.json").read()
except FileNotFoundError as e:
    raise RuntimeError("配置文件缺失") from e
```

- `raise ... from e`：显式链，traceback 里能看到原始异常，定位快。
- 直接 `raise RuntimeError(...)`：隐式链，Python 也会把原始异常附在 `__context__` 里，但意图不如 from 明确。
- 函数里捕获后想原样往上抛，用 bare `raise`，不要 `raise e`（会丢掉原始 traceback）。
