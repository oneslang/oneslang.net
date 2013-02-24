---
layout: page
title: 解惑
---

### 变参传递：需要使用...
{% highlight go %}
func Info(v ...interface{}) {
	fmt.Println(v)    // 错误写法
	fmt.Println(v...) // 正确写法
}
{% endhighlight %}

