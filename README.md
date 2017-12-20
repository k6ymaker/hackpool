# HackPool

非常优雅的协程库

## Example


```go
package main

import (
	"fmt"
)

func main() {

	var hp *HackPool
	numGoroutine := 2
	taskCount := 100

	hp = hackpool.New(numGoroutine, func(i interface{}) {
		fmt.Println(i.(int))
	})

	go func() {

		for i := 0; i < taskCount; i++ {
			hp.Push(i)
		}

		// 必须关闭,不然阻塞死锁
		hp.Close()
	}()

	// 跑起来! 伙计
	hp.Run()
}
```

## Installation

    go get github.com/dean2020/hackpool

## License

This project is copyleft of [CSOIO](http://www.csoio.com/) and released under the GPL 3 license.

