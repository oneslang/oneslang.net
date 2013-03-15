---
layout: page
title: 解惑
---

### 变参传递：需要使用...
{% highlight go %}
func Info(v ...interface{}) {
	println(v)    // 错误写法
	println(v...) // 正确写法
}
{% endhighlight %}

