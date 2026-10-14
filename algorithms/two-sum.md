# 算法：两数之和，哈希表一次遍历

## 暴力是 O(n²)，哈希表是 O(n)

```python
def two_sum(nums, target):
    seen = {}  # 值 -> 下标
    for i, x in enumerate(nums):
        need = target - x
        if need in seen:
            return [seen[need], i]
        seen[x] = i
    return []
```

边遍历边存，查 `target - x` 在不在表里，
一次遍历搞定。

## 为什么先查再存

```python
nums = [3, 3], target = 6
```

如果先存再查，`i=0` 时查 `6-3=3`，
会查到自己。先查后存保证配对的是**之前**的元素。

## 变形：三数之和

排序 + 固定一个 + 双指针，O(n²)。
注意去重：跳过相同的固定位和相同的左指针。

## 哈希表的通用套路

"找配对""判重复""计数"，先想哈希表：

```python
from collections import Counter
Counter("aabbc")  # {'a': 2, 'b': 2, 'c': 1}
```

空间换时间，面试和工程里都高频。
