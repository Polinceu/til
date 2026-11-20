# Rust：String 和 &str，拥有还是借用

新手最常卡住的地方：什么时候用 `String`，什么时候用 `&str`。

## 一句话区分

- `String`：拥有所有权、可变、堆上分配，能 `push_str`。
- `&str`：借来的字符串切片，只读、可以是字面量也可以是 `String` 的一部分。

```rust
let s = String::from("hello");
let slice: &str = &s[..];       // 从 String 借一个 &str
let lit: &str = "world";        // 字面量本身就是 &str

fn greet(name: &str) { println!("hi {}", name); }
greet(&s);   // &String 会自动解引用成 &str
greet(lit);
```

## 参数类型选 &str 的好处

- 函数参数写 `&str`，调用方传 `String` 和字面量都行；写 `String` 就只能传 `String`。
- 返回值需要"新造"字符串才用 `String`，否则优先返回 `&str`。

## 注意

- `&str` 不能按字节下标取：`s[0]` 编译不过，UTF-8 一个字符占多个字节，
  要取字符用 `s.chars().nth(0)`，取切片用 `&s[0..2]`（且必须落在字符边界上）。
