---
layout: page
title: 并发
---

### 概念
<ul>
<li>Go使用channel和goroutine开发并行程序</li>
<li>利用<code>runtime.GOMAXPROCS(n)</code>可以设置goroutine并行执行的数量</li>
<li><code>ch := make(chan type, value)</code>当value == 0时为无缓冲的阻塞的</li>
<li><code>ch := make(chan type, value)</code>当value > 0时为缓冲的非阻塞的</li>
</ul>

### goroutine
{% highlight java %}
ready("Tea", 2) // 普通函数调用
go ready("Tea", 2) // 作为goroutine运行
{% endhighlight %}

### channel
{% highlight java %}
ci := make(chan int)
ci <- 1   // 发送整数1到channel ci
<-ci      // 从channel ci 接收整数
i := <-ci // 从channel ci 接收整数，并保存到i中
{% endhighlight %}

### select
{% highlight java %}
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


