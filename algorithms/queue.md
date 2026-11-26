# 算法：队列，deque 比 list 快

```python
from collections import deque

q = deque()
q.append(1)      # 队尾入队
q.append(2)
print(q.popleft())  # 1，队首出队

# 滑动窗口：固定长度的队列
w = deque(maxlen=3)
for x in [1, 2, 3, 4]:
    w.append(x)
print(list(w))  # [2, 3, 4]
```

- `list.pop(0)` 是 O(n)，`deque.popleft()` 是 O(1)，队列场景别用 list。
- `maxlen` 的 deque 满了会自动丢最旧的，滑动窗口很方便。
- BFS、任务队列、消息缓冲，底层都是队列。
