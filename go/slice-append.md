# Go：slice 的 append 和底层数组共享

## append 可能返回新数组

```go
s := make([]int, 0, 2)
fmt.Println(len(s), cap(s))  // 0 2

s = append(s, 1, 2)
fmt.Println(len(s), cap(s))  // 2 2

s = append(s, 3)             // 容量不够，分配新数组
fmt.Println(len(s), cap(s))  // 3 4（翻倍）
```

**必须用返回值接住**：`s = append(s, x)`，
不接的话扩容就丢了，这是新手最高频的 bug。

## 切片共享底层数组的坑

```go
a := []int{1, 2, 3, 4}
b := a[1:3]   // b 是 [2 3]，和 a 共享底层数组
b[0] = 99
fmt.Println(a)  // [1 99 3 4]，a 也被改了！
```

子切片不是拷贝，改 b 会影响 a。想要独立拷贝：

```go
c := append([]int{}, a[1:3]...)
// 或者 Go 1.21+：c := slices.Clone(a[1:3])
```

## 预分配容量

事先知道大概多大，用 `make([]T, 0, n)` 预分配，
避免反复扩容搬运，循环里 append 快不少。
