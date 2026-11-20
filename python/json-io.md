# Python：json 读写，别忘了 ensure_ascii

```python
import json

data = {"name": "小明", "tags": ["a", "b"]}

# 写：中文直接存，不转 \uXXXX
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

# 读
with open("data.json", encoding="utf-8") as f:
    print(json.load(f))

# 字符串互转
s = json.dumps(data, ensure_ascii=False)
print(json.loads(s))
```

- `ensure_ascii=False` 不加，中文会变成 `\u5c0f\u660e`，人看不懂。
- `indent=2` 让文件可读；不加就是一行，省空间。
- `json.load` 读文件，`json.loads` 读字符串，别混用。
