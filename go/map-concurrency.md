# Go：map 不是并发安全的，多个 goroutine 写会直接 crash

Go 的 map 读写没有锁，两个 goroutine 同时写一个 map，运行时会报
`fatal error: concurrent map writes`，连 recover 都救不回来。

## 互斥锁包一层

```go
type SafeCounter struct {
    mu sync.Mutex
    m  map[string]int
}

func (c *SafeCounter) Inc(key string) {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.m[key]++
}
```

## 或者用 sync.Map

```go
var m sync.Map
m.Store("a", 1)
v, ok := m.Load("a")   // ok 表示在不在
m.Range(func(k, v any) bool {
    fmt.Println(k, v)
    return true        // 返回 false 会提前停
})
```

## 选哪个

- 读多写少、key 固定：`sync.Map` 方便。
- 逻辑复杂（读-改-写要原子）：自己加 `sync.RWMutex`，读锁 `RLock`、写锁 `Lock`。
- 顺带记：map 遍历顺序是随机的，别依赖它；`delete(m, k)` 删不存在的 key 不报错。
