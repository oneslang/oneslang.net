---
layout: page
title: 解惑
---

### 概念
* 变参传递需要使用`...`
* 在同一`goroutine`对同一无缓冲的`channel`即执行发送操作又执行接受操作会出现死锁
* 当`main`函数返回时程序直接退出，并不会管其他`goroutine`是否执行完

### 变参传递：需要使用...
{% highlight go %}
func Info(v ...interface{}) {
	println(v)    // 错误写法
	println(v...) // 正确写法
}
{% endhighlight %}

### deadlock死锁
{% highlight go %}
package main
func main() {
	c := make(chan int)
	c <- 0
	println(<-c)
}
{% endhighlight %}
上面的程序会提示deadlock死锁编译错误，
对channel执行发送操作或者接受操作会阻塞goroutine，
所以在同一goroutine对同一无缓冲的channel即执行发送操作又执行接受操作会出现死锁，
发送和接受操作必须在不同的goroutine中，如下代码：
{% highlight go %}
package main
func receive(c chan int) {
	c <- 0
}
func main() {
	c := make(chan int)
	go receive(c)
	println(<-c)
}
{% endhighlight %}

### goroutine执行顺序
{% highlight go %}
package main
func main() {
	go func() {
		println("oneslang")
	}()
}
{% endhighlight %}
执行上面的程序为什么没有输出oneslang？
那是因为当main函数返回时程序直接退出，并不会管其他goroutine是否执行完，
最简单的解决方式就是让main等待其他goroutine执行完再退出
{% highlight go %}
package main
import "time"
func main() {
	go func() {
		println("oneslang")
	}()
	time.Sleep(1 * 1e9)
}
{% endhighlight %}

