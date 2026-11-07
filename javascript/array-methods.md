# JS：map / filter / reduce 一句话分工

```js
const nums = [1, 2, 3, 4];
nums.map(x => x * 2);        // [2, 4, 6, 8] 转换
nums.filter(x => x % 2 === 0); // [2, 4] 过滤
nums.reduce((s, x) => s + x, 0); // 10 聚合
```

- `map` 和 `filter` 都返回新数组，不改原数组；`sort` 和 `splice` 是原地改，混用时容易出 bug。
- 链式调用可读性好，但每步都产生中间数组，超大数组上注意性能。
- `find` 找到第一个就停，`filter` 会扫完全部；只要一个结果时优先 `find`。
