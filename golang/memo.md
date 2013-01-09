---
layout: page
title: 备忘
---

### 按位与、按位或运算符经典用法
{% highlight java %}
// 以golang的log包为例
const (
	//	2009/01/23 01:23:23.123123 /a/b/c/d.go:23: message
	Ldate         = 1 << iota     // the date: 2009/01/23
	Ltime                         // the time: 01:23:23
	Lmicroseconds                 // microsecond resolution: 01:23:23.123123.  assumes Ltime.
	Llongfile                     // full file name and line number: /a/b/c/d.go:23
	Lshortfile                    // final file name element and line number: d.go:23. overrides Llongfile
	LstdFlags     = Ldate | Ltime // initial values for the standard logger
)

// log通过flag属性控制日志输出格式：多个值使用按位或|运算符
log.SetFlags(log.LstdFlags | log.Lshortfile)                // 设置后输出格式类似：2009/01/23 01:23:23 d.go:23: message
log.SetFlags(log.Ldate | log.Lmicroseconds | log.Llongfile) // 设置后输出格式类似：2009/01/23 01:23:23.123123 /a/b/c/d.go:23: message

// log怎么判断日志输出格式呢：通过按位与&运算符判断
if l.flag&Ldate != 0 { // l是*log.Logger
	// 表示log的flag属性设置了Ldate
}
if l.flag&(LstdFlags|Lshortfile) != 0 {
	// 表示log的flag属性设置了LstdFlags和Lshortfile
}
{% endhighlight %}

### 变参传递方法
{% highlight java %}
func Info(v ...interface{}) {
	fmt.Println(v)    // 错误写法
	fmt.Println(v...) // 正确写法
}
{% endhighlight %}

### 遍历文件夹
{% highlight java %}
filepath.Walk("./usr", func(subpath string, f os.FileInfo, err error) error {
	if err != nil {
		return err
	}
	if f.IsDir() == false {
		fmt.Println(f.Name())
	}
	return nil
})
{% endhighlight %}

