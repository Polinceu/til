# Rust：切片

```rust
fn main() {
    let v = vec![1, 2, 3, 4, 5];
    let s = &v[1..3];   // 切片：[2, 3]
    println!("{:?} {}", s, s.len());

    let text = "hello world";
    let w = &text[0..5];  // "hello"
    println!("{}", w);
}
```

- 切片是对一段连续数据的"视图"，不复制，不拥有。
- `&v[1..3]` 左闭右开，取下标 1、2，不含 3。
- 字符串切片必须切在字符边界上，切在中文中间会 panic。
