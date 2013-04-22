---
layout: page
category: golang
name: interface
title: 接口
---

### 概念
* 无须明确一个类型是否实现了一个接口
* 实现接口使用方法，不能用函数
* 每个类型都能匹配到空接口`interface{}`
* 在switch之外使用类型判断`.(type)`是非法的
* 类型判断`v.(type)`的v是interface或者interface{}
* 类型断言`.(I)`
* 类型断言`v.(I)`的v是interface或者interface{}
* 类型断言`v.(I)`的I是interface或者struct或者pointer等
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
type S struct{ i int }
func (me *S) Get() int  { return me.i }
func (me *S) Set(v int) { me.i = v }

type R struct{ i int }
func (me *R) Get() int  { return me.i }
func (me *R) Set(v int) { me.i = v }
{% endhighlight %}

### 类型判断
{% highlight go %}
var v I = &S{1}
switch t := v.(type) {
case *S:
	fmt.Printf("type:*S,value:%d\n", t.Get())
case *R:
	fmt.Printf("type:*R,value:%d\n", t.Get())
default:
	println("default")
}
{% endhighlight %}


{% highlight go %}
var v interface{} = 1
switch t := v.(type) {
case int:
	fmt.Printf("type:int,value:%d\n", t)
case string:
	fmt.Printf("type:string,value:%s\n", t)
default:
	println("default")
}
{% endhighlight %}

### 类型断言
{% highlight go %}
v := &S{1}
if i, ok := v.(I); ok {
	fmt.Printf("type:I,value:%d\n", i.Get())
} else {
	println("not I")
}
{% endhighlight %}


{% highlight go %}
var v I = &R{1}
if r, ok := v.(*R); ok {
	fmt.Printf("type:*R,value:%d\n", r.Get())
} else {
	println("not *R")
}
{% endhighlight %}

### 空接口
{% highlight go %}
func g(something interface{}) int { // 用空接口作为参数
    return something.(I).Get() // 类型断言
}
{% endhighlight %}

