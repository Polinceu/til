# JS：Promise.all vs Promise.allSettled

## all：一个失败，全部失败

```js
const results = await Promise.all([
  fetch("/api/a"),
  fetch("/api/b"),  // 这个挂了
  fetch("/api/c"),
]);
// 直接抛错，a 和 c 的结果也拿不到
```

适合"缺一不可"的场景：比如同时拉用户信息和权限，少一个页面都渲染不了。

## allSettled：全部等完再说

```js
const results = await Promise.allSettled([
  fetch("/api/a"),
  fetch("/api/b"),
  fetch("/api/c"),
]);

for (const r of results) {
  if (r.status === "fulfilled") console.log(r.value);
  else console.error("挂了:", r.reason);
}
```

返回的每个元素都是 `{ status, value?/reason? }`，不会抛错。

## 怎么选

- 批量请求里有一个失败就整体无意义 → `Promise.all`。
- 批量任务"能成几个是几个"，比如批量发通知、批量查状态 → `allSettled`。
- 还有个 `Promise.any`：只要有一个成功就行，拿第一个成功的结果。

之前图省事全用 all，被一个超时的接口拖累了整个页面，记住了。
