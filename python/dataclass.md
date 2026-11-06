# Python：dataclass 什么时候比 dict 好

```python
from dataclasses import dataclass, field

@dataclass
class User:
    name: str
    age: int = 0
    tags: list = field(default_factory=list)
```

- 字段有类型、有默认值，IDE 能补全，dict 做不到。
- `field(default_factory=list)` 是必须的：直接写 `tags: list = []` 会导致所有实例共享同一个列表。
- 需要不可变时加 `@dataclass(frozen=True)`，字段赋值会直接报错。
- 只是临时传数据、不需要方法时，dict 更轻量，没必要上 dataclass。
