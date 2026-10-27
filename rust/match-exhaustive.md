# Rust：match 必须是穷尽的

## 编译器逼你处理所有情况

```rust
enum Coin { Penny, Nickel, Dime }

fn value(c: Coin) -> u8 {
    match c {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
    }
}
```

少写一个分支就编译不过。这就是"穷尽性检查"，
很多运行时 bug 在这里就被拦下了。

## 通配分支 `_` 和 `..`

```rust
let n = 7;
match n {
    1 => println!("one"),
    2 | 3 => println!("two or three"),  // 或模式
    4..=9 => println!("many"),          // 范围模式
    _ => println!("other"),             // 兜底
}
```

## match 是表达式，有返回值

```rust
let kind = match n {
    1 => "one",
    _ => "other",
};
// 注意：所有分支返回类型必须一致
```

## if let：只关心一种情况

```rust
let opt = Some(5);
if let Some(v) = opt {
    println!("got {}", v);
}
```

只处理 `Some`、忽略 `None` 时比完整 match 省事。
但别滥用：需要处理多种情况时老老实实写 match。
