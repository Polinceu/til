# 算法：贪心入门

```python
# 找零：每次拿面值最大的硬币
def change(amount, coins=(25, 10, 5, 1)):
    out = []
    for c in coins:
        while amount >= c:
            out.append(c)
            amount -= c
    return out

print(change(87))  # [25, 25, 25, 10, 1, 1]
```

- 贪心：每一步都选当前看起来最好的，不管以后。
- 找零这种"面值整齐"的问题贪心是对的，但不一定都对（比如面值 1、3、4，找 6 时贪心给 4+1+1，不如 3+3）。
- 用贪心前先想清楚：局部最优能不能推出全局最优，不能就别用。
