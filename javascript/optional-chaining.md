# JS：`?.` 和 `??`，以及它们和 `||` 的区别

## 可选链：深层取值不再写一串 &&

```js
const user = { profile: { name: "a" } };
console.log(user?.profile?.name);        // "a"
console.log(user?.settings?.theme);       // undefined，不报错
console.log(user?.getName?.());           // 方法可能不存在也安全
```

## 空值合并：只对 null/undefined 生效

```js
const count = 0;
console.log(count || 10);   // 10，0 被当成假值，可惜
console.log(count ?? 10);   // 0，这才是想要的

const name = "";
console.log(name || "匿名");  // "匿名"
console.log(name ?? "匿名");  // ""，空字符串被保留
```

## 经验法则

- 取深层属性、调可能不存在的方法：用 `?.`。
- 给"可能缺失"的配置项设默认值：用 `??`，别用 `||`，
  除非你真的想把 `0`、`""`、`false` 也替换掉。

```js
const port = config.port ?? 3000;  // port 为 0 时保留 0
```

这两个配合起来， defensive code 能少写一大半。
