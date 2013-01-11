---
layout: page
title: 并发
---

### 概念
* Go使用channel和goroutine开发并行程序
* 利用`runtime.GOMAXPROCS(n)`可以设置goroutine并行执行的数量
* `ch := make(chan type, value)`当value == 0时为无缓冲的阻塞的
* `ch := make(chan type, value)`当value > 0时为缓冲的非阻塞的

### goroutine
{% highlight go %}
ready("Tea", 2) // 普通函数调用
go ready("Tea", 2) // 作为goroutine运行
{% endhighlight %}

### channel
{% highlight go %}
ci := make(chan int)
ci <- 1   // 发送整数1到channel ci
<-ci      // 从channel ci 接收整数
i := <-ci // 从channel ci 接收整数，并保存到i中
{% endhighlight %}

### select
{% highlight go %}
package main

import (
    "time"
    "fmt"
)

var c chan int

func ready(w string, sec int) {
    time.Sleep(time.Duration(sec) * time.Second)
    fmt.Println(w, "is ready!")
    c <- 1
}

func main() {
    c = make(chan int)
    go ready("Tea", 2)
    go ready("Coffee", 1)
    fmt.Println("I'm waiting, but not too long")
    i := 0
    L: for {
        select {
            case <-c:
                i++
                if i > 1 {
                    break L
                }
        }
    }
}
{% endhighlight %}


