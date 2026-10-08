# Go：用 %w 包装错误，别丢了错误链

## 问题：fmt.Errorf 会断掉错误链

```go
if err != nil {
    return fmt.Errorf("读取配置失败: %v", err)  // %v：只转成字符串
}
// 调用方没法再判断原始错误类型
```

## 解法：%w 保留包装关系

```go
import "errors"

var ErrNotFound = errors.New("not found")

func load(id string) error {
    // ...
    return fmt.Errorf("load %s: %w", id, ErrNotFound)
}

err := load("a")
fmt.Println(errors.Is(err, ErrNotFound))  // true，能透过包装认出来
```

## errors.Is / errors.As 的分工

- `errors.Is`：判断"是不是某个哨兵错误"（== 的链式版）。
- `errors.As`：把错误链里"第一个匹配类型的"取出来：

```go
var pathErr *os.PathError
if errors.As(err, &pathErr) {
    fmt.Println("路径:", pathErr.Path)
}
```

## 习惯

- 包内定义的固定错误用 `var ErrXxx = errors.New(...)`。
- 往上抛时用 `%w` 加上下文，别用 `%v` 裸转字符串。
- 最外层统一打印完整链，中间层只包装不打印（避免重复日志）。
