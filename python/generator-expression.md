# Python：列表推导式 vs 生成器表达式

处理大文件时又被内存教做人了，记录一下。

## 写法上只差一对括号

```python
squares = [x * x for x in range(10)]      # 列表：一次全算出来
squares_gen = (x * x for x in range(10))   # 生成器：用到才算
```

## 内存差异

```python
import sys

lst = [x for x in range(1000000)]
gen = (x for x in range(1000000))
print(sys.getsizeof(lst))  # 约 8MB
print(sys.getsizeof(gen))   # 约 200 字节，和数据量无关
```

生成器不保存所有元素，只记住"算到哪了"，所以内存占用是常数级的。

## 什么时候用哪个

- 只消费一次的聚合（`sum` / `max` / `any` / `join`），直接传生成器：

```python
total = sum(x * x for x in range(10**7))  # 不会爆内存
```

- 需要反复遍历、取下标、`len()` 的时候，才用列表。

小结：数据只遍历一次，就别急着转成 list，括号换一下就行。
