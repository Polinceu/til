# Rust：Option / Result 与 `?` 操作符

Rust 没有 null，"可能没有值"和"可能出错"都用枚举显式表达。

## Option：可能没有值

```rust
fn find_user(id: u32) -> Option<String> {
    if id == 1 { Some("alice".to_string()) } else { None }
}

match find_user(2) {
    Some(name) => println!("found {}", name),
    None => println!("not found"),
}
```

## Result：可能出错

```rust
use std::fs;

fn read_config() -> Result<String, std::io::Error> {
    fs::read_to_string("config.toml")
}
```

## `?`：错误向上传播的语法糖

```rust
fn load() -> Result<String, std::io::Error> {
    let s = fs::read_to_string("a.txt")?;  // 出错直接 return Err
    let t = fs::read_to_string("b.txt")?;  // 正常则解包出 String
    Ok(s + &t)
}
```

`?` 只能用在返回 Result/Option 的函数里，
相当于"有值就拆出来，没值就提前返回"。

## 常用组合子

```rust
let n: Option<i32> = Some(5);
let m = n.map(|x| x * 2);              // Some(10)
let k: Option<i32> = None;
let v = k.unwrap_or(0);                // None 时给默认值 0
```

`unwrap()` 会在 None/Err 时 panic，只在"绝不可能失败"时用，
比如测试代码。正式代码多用 `?` 和 `unwrap_or`。
