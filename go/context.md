# Go：context 是用来传取消信号的，不是传数据的

```go
ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
defer cancel()

req, _ := http.NewRequestWithContext(ctx, "GET", url, nil)
resp, err := http.DefaultClient.Do(req)
```

- 超时、取消用 context；业务数据（用户 ID、请求 ID）也可以放，但别放核心业务对象。
- `defer cancel()` 一定要写，否则计时器会泄漏到超时才释放。
- 不要把 context 存到 struct 字段里，函数参数显式传。
- `context.Background()` 只在 main 和测试顶层用，库函数里接调用方传进来的 ctx。
