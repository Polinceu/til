# Python：f-string 的 `=` 调试语法真香

Python 3.8+ 的 f-string 支持 `=` 后缀，调试时少写一半 print。

## 基础用法

```python
x = 10
y = 20
print(f"{x=}, {y=}")        # x=10, y=20
print(f"{x + y = }")        # x + y = 30
```

变量名、等号、值一次打印出来，不用再手写 `"x ="` 这种前缀。

## 配合格式说明符

```python
pi = 3.1415926
print(f"{pi=:.2f}")         # pi=3.14

from datetime import datetime
now = datetime.now()
print(f"{now=:%Y-%m-%d}")   # now=2026-10-02
```

`=` 写在前面，`:.2f` 这种格式控制写在后面，两者不冲突。

## 还有两个冷门的

```python
n = 255
print(f"{n=:b}")   # n=11111111，二进制
print(f"{n=:x}")   # n=ff，十六进制
```

不过正式日志里还是别用，`=` 语法是给人看的，机器解析不友好。
