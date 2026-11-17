# Python：pathlib 替代 os.path，路径拼接不再拼字符串

`os.path.join(a, b)` 写多了容易漏斜杠，`pathlib.Path` 用 `/` 拼接，可读性好得多。

## 常用写法

```python
from pathlib import Path

p = Path("data") / "2026" / "report.txt"
print(p.exists())          # 文件在不在
print(p.parent)            # data/2026
print(p.suffix)            # .txt
print(p.stem)              # report
text = p.read_text(encoding="utf-8")   # 直接读，不用 open
```

## 几个顺手操作

```python
Path("out").mkdir(parents=True, exist_ok=True)  # 递归建目录，已存在不报错
for f in Path("data").glob("*.md"):             # 通配符找文件
    print(f)
p.rename(p.with_suffix(".bak"))                 # 改后缀就是改名
```

## 和旧代码混用

- 需要字符串时：`str(p)`，大部分标准库函数直接接受 `Path` 对象。
- `Path.home()` 拿家目录，`Path.cwd()` 拿当前目录，比 `os.path.expanduser("~")` 好记。
- 注意：`/` 拼接时如果右边是绝对路径，左边会被丢弃，`Path("/a") / "/b"` 得到 `/b`。
