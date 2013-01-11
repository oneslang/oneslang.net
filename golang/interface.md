---
layout: page
title: 接口
---

### 概念
* 无须明确一个类型是否实现了一个接口
* 实现接口使用方法，不能用函数
* 每个类型都能匹配到空接口`interface{}`
* 在switch之外使用类型判断`.(type)`是非法的
* 类型断言`.(I)`
* 单方法接口命名为方法名加上-er，例如Reader,Writer,Formatter等

### 定义接口
{% highlight go %}
type I interface {
    Get() int
    Put(int)
}
{% endhighlight %}

### 实现接口
{% highlight go %}
type S struct { i int }
func (p *S) Get() int { return p.i }
func (p *S) Put(v int) { p.i = v }

type R struct { i int }
func (p *R) Get() int { return p.i }
func (p *R) Put(v int) { p.i = v }
{% endhighlight %}

### 类型判断
{% highlight go %}
func f(p I) {
    switch t := p.(type) {
        case *S:
        case *R:
        case S:
        case R:
        default:
    }
}
{% endhighlight %}

### 类型断言
{% highlight go %}
if t, ok := something.(I); ok {
    // 对于某些实现了接口I 的
    // t 是其所拥有的类型
}
{% endhighlight %}

### 空接口
{% highlight go %}
func g(something interface{}) int { // 用空接口作为参数
    return something.(I).Get() // 类型断言
}
{% endhighlight %}

