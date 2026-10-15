# Python：dict.setdefault 和 defaultdict 到底用哪个

今天写词频统计，又在 `d[k] = d.get(k, 0) + 1` 和 defaultdict 之间犹豫，干脆记下来。

## setdefault：字典自带的写法

```python
counts = {}
for w in ["apple", "banana", "apple"]:
    counts[w] = counts.get(w, 0) + 1
print(counts)  # {'apple': 2, 'banana': 1}
```

`setdefault(key, default)` 的语义是"key 不存在就设为 default，并返回它"：

```python
groups = {}
for name, team in [("a", "x"), ("b", "y"), ("c", "x")]:
    groups.setdefault(team, []).append(name)
print(groups)  # {'x': ['a', 'c'], 'y': ['b']}
```

## defaultdict：需要"工厂函数"的场景

```python
from collections import defaultdict

groups = defaultdict(list)
for name, team in data:
    groups[team].append(name)  # 不存在的 key 自动创建一个 []
```

## 我的选择

- 简单计数、分组：`defaultdict` 写起来更干净。
- 偶尔查一次、默认值是不可变对象：`setdefault` 就够了，不用 import。
- 注意副作用：`defaultdict` 访问不存在的 key 会**创建**它，
  所以 `if k in d` 这种判断要小心，别先触发了自动创建。

小坑：`defaultdict(list)` 传的是工厂函数，别写成 `defaultdict([])`，
后者会直接报错。
