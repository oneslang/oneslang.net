---
layout: page
title: 解惑
---

### 概念
* 变参传递需要使用`...`
* 当`main`函数返回时程序直接退出，并不会管其他`goroutine`是否执行完

### 变参传递：需要使用...
{% highlight go %}
func Info(v ...interface{}) {
	println(v)    // 错误写法
	println(v...) // 正确写法
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

