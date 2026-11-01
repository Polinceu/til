# TypeScript：最常用的四个工具类型

```ts
interface User { id: number; name: string; email: string; }

// 全部可选
type PartialUser = Partial<User>;
// 只留 id 和 name
type Picked = Pick<User, "id" | "name">;
// 去掉 email
type WithoutEmail = Omit<User, "email">;
// 所有字段只读
type Frozen = Readonly<User>;
```

- 写更新接口时 `Partial<User>` 比手写一堆 `?` 省事。
- `Pick` 和 `Omit` 是互补的：字段少用 Pick，字段多用 Omit。
- `Record<string, User>` 可以快速建字典类型，key 的类型要写全。
