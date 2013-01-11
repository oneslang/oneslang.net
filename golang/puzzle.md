---
layout: page
title: 解惑
---

### 变参传递：需要使用...
{% highlight java %}
func Info(v ...interface{}) {
	fmt.Println(v)    // 错误写法
	fmt.Println(v...) // 正确写法
}
{% endhighlight %}

### 递归结构：必须使用指针类型
{% highlight java %}
type Org struct {
	Name   string
	Parent Org  // 错误写法
	Parent *Org // 正确写法
}
{% endhighlight %}

