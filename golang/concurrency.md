---
layout: page
title: 并发
---

### 概念
* Go使用`goroutine`和`channel`开发并行程序
* `c := make(chan type, value)`当value == 0时为无缓冲的阻塞的，当value > 0时为缓冲的非阻塞的
* 使用`close`函数关闭channel
* 通过`v, ok := <-c`语句测试channel是否被关闭
* 单个缓冲channel通过`for v := range c`语句能够不断的读取channel里面的数据，直到该channel被显式的关闭
* 多个channel使用`select`监听channel上的数据流动
* `select`的`case`语句必须是面向channel的操作
* 利用`runtime.GOMAXPROCS(n)`可以设置goroutine并行执行的数量
* 利用`runtime.NumCPU()`可以获取CPU的数量

### goroutine
{% highlight go %}
ready("Tea", 2) // 普通函数调用
go ready("Tea", 2) // 作为goroutine运行
{% endhighlight %}

### channel
{% highlight go %}
c := make(chan int)
c <- 1   // 发送整数1到channel c
<-c      // 从channel c 接收整数
i := <-c // 从channel c 接收整数，并保存到i中
{% endhighlight %}

### buffered
{% highlight go %}
c := make(chan int, 2) // 修改2为1就报错，修改2为3可以正常运行
c <- 1
c <- 2
fmt.Println(<-c)
fmt.Println(<-c)
{% endhighlight %}

### range
{% highlight go %}
c := make(chan int, 2)
c <- 1
c <- 2
for v := range c {
	fmt.Println(v)
}
{% endhighlight %}

### close
{% highlight go %}
c := make(chan int)
c <- 1
close(c)
{% endhighlight %}

### select
{% highlight go %}
select {
case <-chan1:
    // 如果chan1成功读到数据执行
case chan2 <- 1:
    // 如果成功向chan2写入数据执行
default:
    // 如果上面都没有成功执行
}
{% endhighlight %}

