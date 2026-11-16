# Python：枚举 Enum，别再用裸字符串当状态了

状态字段写 `"pending"`、`"done"` 这种裸字符串，拼错一个字母就静默出错，改记 Enum。

## 基本写法

```python
from enum import Enum, auto

class Status(Enum):
    PENDING = auto()
    RUNNING = auto()
    DONE = auto()

s = Status.PENDING
print(s.name)   # PENDING
print(s.value)  # 1（auto() 自动编号）
print(Status(1))  # Status.PENDING，可以从值反查
```

## 三个实用点

- 比较用 `is`：`if s is Status.DONE:`，枚举成员是单例。
- 需要和数字比大小、存数据库：用 `IntEnum`，`Status.DONE == 3` 成立。
- 遍历：`list(Status)` 按定义顺序；`Status.__members__` 是名字到成员的字典。

## 别踩的坑

- 成员值重复会被当作**别名**：两个名字同一个值，遍历时只出现第一个。
  想要允许重复值，用 `Flag` 或者干脆别用 Enum。
- 不要拿 Enum 成员直接 `json.dumps`，它不是基本类型，先取 `.value` 或 `.name`。
