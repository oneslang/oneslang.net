---
layout: page
category: golang
name: function
title: 函数
---

### 概念
* Go不允许函数嵌套，可以利用匿名函数实现
* 函数外定义变量是全局的，函数内部定义变量对于函数来说是局部的
* 局部变量和全局变量名称相同时，局部变量将覆盖全局变量
* 延迟函数是按照后进先出的顺序执行

### 作用域
{% highlight go %}
package main
var a = 6
func main() {
    p()
    q()
    p()
}
func p() {
    println(a) // 输出6
}
func q() {
    a := 5
    println(a) // 输出5
}
{% endhighlight %}

### 多个返回值
{% highlight go %}
func nextInt(b []byte, i int) (int, int) {
    x := 0
    // 假设所有的都是数字
    for ; i < len(b); i++ {
        x = x*10 + int(b[i])-'0'
    }
    return x, i
}
{% endhighlight %}

### 命名返回参数
{% highlight go %}
func ReadFull(r Reader, buf []byte) (n int, err os.Error) {
    for len(buf) > 0 && err == nil {
        var nr int
        nr, err = r.Read(buf)
        n += nr
        buf = buf[nr:len(buf)]
    }
    return
}
{% endhighlight %}

### 延迟的代码
{% highlight go %}
func ReadWrite() bool {
    file.Open("file")
    defer file.Close()
    if failureX {
        return false // 自动调用file.Close()
    }
    if failureY {
        return false // 自动调用file.Close()
    }
    return true
}

defer func() {
}()    // ()在这里是必须的

defer func(x int) {
}(5)   // 为输入参数x赋值5
{% endhighlight %}

### 变参
{% highlight go %}
func myfunc(arg ...int) {}
    for _, n := range arg {
        fmt.Printf("And the number is: %d\n", n)
    }
}
{% endhighlight %}

### 函数作为值
{% highlight go %}
func main() {
    a := func() {   // 定义一个匿名函数，并且赋值给a
        println("Hello")
    }
    a()   // 调用函数
}
{% endhighlight %}

### 回调
{% highlight go %}
func callback(y int, f func(int)) {   // f 将会保存函数
    f(y)   // 调用回调函数f 输入变量y
}
{% endhighlight %}

### 恐慌（Panic）和恢复（Recover）
{% highlight go %}
func throwsPanic(f func()) (b bool) {
    defer func() {
        if x := recover(); x != nil {
            b = true
        }
    }()
    f()
    return
}
{% endhighlight %}


