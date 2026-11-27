# JS：空值合并 ?? 和可选链 ?.

```js
const port = config.port ?? 3000;   // 只有 null/undefined 才用默认值
const name = user?.profile?.name;   // 链上任何一环是空就返回 undefined

// 对比：|| 会把 0、""、false 也当成空
const n = 0 || 10;   // 10（可能不是你想要的）
const m = 0 ?? 10;   // 0
```

- `??` 只认 `null` 和 `undefined`，`0`、`""`、`false` 都会保留。
- `?.` 遇到空直接停，不会抛 `Cannot read properties of undefined`。
- `??` 不能和 `||`/`&&` 混写不加括号，语法会报错。
