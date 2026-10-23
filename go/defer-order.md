# Go：defer 是后进先出，别写反了

## 基本规则：LIFO

```go
package main

import "fmt"

func main() {
    defer fmt.Println("1")
    defer fmt.Println("2")
    defer fmt.Println("3")
}
// 输出：3 2 1
```

像栈一样，后注册的先执行。关资源时一般按"后开先关"写，正好对上。

## 参数是立即求值的

```go
func main() {
    i := 0
    defer fmt.Println(i)  // 注册时 i=0，打印 0
    i = 1
    fmt.Println(i)        // 打印 1
}
```

defer 后面函数的**参数在 defer 语句执行时就求值**了，
不是等到函数返回时才求值。这个坑踩过一次就记住了。

## 经典用途：具名返回值 + 修改

```go
func readAll() (err error) {
    f, err := os.Open("a.txt")
    if err != nil {
        return err
    }
    defer f.Close()
    defer func() {
        if r := recover(); r != nil {
            err = fmt.Errorf("panic: %v", r)
        }
    }()
    // ... 读取逻辑
    return nil
}
```

defer + recover 是 Go 里"异常处理"的标准姿势，
记得 recover 必须在 defer 注册的函数里直接调。
