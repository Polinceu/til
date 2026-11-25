# 算法：栈，括号匹配的经典题

```python
def valid(s):
    pairs = {")": "(", "]": "[", "}": "{"}
    st = []
    for ch in s:
        if ch in "([{":
            st.append(ch)
        elif ch in ")]}":
            if not st or st.pop() != pairs[ch]:
                return False
    return not st

print(valid("()[]{}"))  # True
print(valid("([)]"))    # False
```

- 栈是后进先出，括号匹配、表达式求值、函数调用栈都是它。
- Python 里 list 就是栈：`append` 入栈，`pop` 出栈。
- 出栈前先判空，不然 `pop` 空列表会抛错。
