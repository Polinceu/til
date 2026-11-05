# JS：async/await 的几个容易踩的点

```js
// 串行：一个接一个，总耗时相加
const a = await fetchA();
const b = await fetchB();

// 并行：一起出发，总耗时取最长那个
const [x, y] = await Promise.all([fetchA(), fetchB()]);
```

- `await` 只会暂停当前 async 函数，不会阻塞整个线程。
- 循环里 `await` 会把并行活干成串行，能并行的先收集 Promise 再 `Promise.all`。
- `Promise.all` 一个失败就全失败，需要各自容错时用 `Promise.allSettled`。
