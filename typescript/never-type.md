# TypeScript：never 类型的实际用途

`never` 表示"永远不会出现的值"，听起来玄，实际就两个用处。

## 用处一：穷尽检查（exhaustive check）

```ts
type Shape = "circle" | "square";

function area(s: Shape): number {
  switch (s) {
    case "circle": return 3.14;
    case "square": return 1;
    default:
      const _exhaustive: never = s;  // 如果 Shape 加了新成员，这里编译报错
      throw new Error(`unknown shape: ${_exhaustive}`);
  }
}
```

以后给 `Shape` 加 `"triangle"` 却忘了写分支，编译器会直接拦下来。
这比运行时才发现强太多。

## 用处二：不可能返回的函数

```ts
function fail(msg: string): never {
  throw new Error(msg);
}

function infinite(): never {
  while (true) {}
}
```

标注 `never` 后，调用方后面的代码会被识别为不可达，
有些 lint 规则能顺手帮你发现逻辑问题。

## 和 void 的区别

- `void`：函数正常返回，只是不带值。
- `never`：函数根本不会正常返回（抛错或死循环）。

一句话：想让编译器帮你"查漏"，就用 never 做穷尽检查。
