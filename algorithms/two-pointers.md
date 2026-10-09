# 算法：快慢指针，一个套路解三类题

## 1. 判断链表是否有环

```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow is fast:
            return True
    return False
```

快的每次走两步，追上慢的就是有环。O(1) 空间。

## 2. 找环的入口（进阶）

相遇后，把一个指针放回 head，两边同速走，
再次相遇就是入口。数学证明略，记住结论。

## 3. 有序数组原地去重

```python
def remove_duplicates(nums):
    slow = 0
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    return slow + 1
```

slow 指向"已处理好的末尾"，fast 探路，
不一样就把 fast 的值搬到 slow+1。

## 本质

快慢指针 = 用两个不同速度/角色的索引，
把 O(n) 空间的问题压成 O(1)。
看到"链表环""原地""有序"，先想它。
