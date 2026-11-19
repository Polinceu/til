# JS：fetch 没有自带超时，用 AbortController 自己加

`fetch` 只会在断网时 reject，服务器一直不回，它能一直等下去，超时要自己实现。

## 固定写法

```js
async function fetchWithTimeout(url, ms = 5000) {
  const ctrl = new AbortController();
  const timer = setTimeout(() => ctrl.abort(), ms);
  try {
    const res = await fetch(url, { signal: ctrl.signal });
    if (!res.ok) throw new Error("HTTP " + res.status);
    return await res.json();
  } finally {
    clearTimeout(timer); // 成功也要清掉定时器，别留着
  }
}
```

## 注意点

- 超时后抛出的错误名是 `AbortError`，可以 `err.name === "AbortError"` 单独处理。
- `fetch` 只有网络层失败才 reject，404/500 都会 resolve，要自己检查 `res.ok`。
- 同一个 `AbortController` 可以取消多个请求，适合"页面切走就全停"的场景。
