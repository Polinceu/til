# JS：setTimeout 和 setInterval

```js
const id = setTimeout(() => console.log("1 秒后执行"), 1000);
clearTimeout(id);  // 取消

let n = 0;
const timer = setInterval(() => {
  n += 1;
  console.log(n);
  if (n >= 3) clearInterval(timer);  // 记得停，不然一直跑
}, 500);
```

- `setTimeout` 只跑一次，`setInterval` 每隔一段时间跑一次。
- 两个都返回 id，`clearTimeout/clearInterval` 用 id 取消。
- 回调里如果忘了 `clearInterval`，定时器会一直跑到页面关闭。
