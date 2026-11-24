# Go：flag 解析命令行参数

```go
package main

import (
	"flag"
	"fmt"
)

func main() {
	name := flag.String("name", "world", "要问候的人")
	n := flag.Int("n", 1, "问候几次")
	flag.Parse()
	for i := 0; i < *n; i++ {
		fmt.Println("hello", *name)
	}
}
```

- `flag.String` 返回的是指针，用的时候要 `*name` 解引用。
- `flag.Parse()` 必须调，不然参数都读不到。
- `go run main.go -name tom -n 2`，没传的参数用默认值。
