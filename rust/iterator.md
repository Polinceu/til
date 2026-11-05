# Rust：迭代器是惰性的，不消费就不干活

```rust
let v = vec![1, 2, 3, 4];
let sum: i32 = v.iter().filter(|&&x| x % 2 == 0).map(|x| x * 2).sum();
```

- `iter()` 借用元素，`into_iter()` 拿走所有权，`iter_mut()` 可变借用。
- 适配器（map、filter）只是搭链子，调用 `collect`、`sum` 这类消费方法时才真正执行。
- `collect::<Vec<_>>()` 需要注明目标类型，否则编译器推不出来。
