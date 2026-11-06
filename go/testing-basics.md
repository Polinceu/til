# Go：表驱动测试是标准写法

```go
func TestAdd(t *testing.T) {
    cases := []struct {
        a, b, want int
    }{
        {1, 2, 3},
        {-1, 1, 0},
        {0, 0, 0},
    }
    for _, c := range cases {
        if got := Add(c.a, c.b); got != c.want {
            t.Errorf("Add(%d, %d) = %d, want %d", c.a, c.b, got, c.want)
        }
    }
}
```

- 测试文件以 `_test.go` 结尾，函数名以 `Test` 开头，参数是 `*testing.T`。
- `go test ./...` 跑整个模块，`-run` 可以只跑匹配的测试。
- 表驱动的好处：加用例就是加一行，不用复制测试函数。
