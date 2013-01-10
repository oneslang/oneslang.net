---
layout: page
title: 包
---

### 概念
* 包是函数和数据的集合
* 文件名不需要与包名一致
* 包可以由多个文件组成
* 包名用的是根目录名：在src/pkg/compress/gzip的包，作为compress/gzip导入，但名字是gzip
* 首字母大写：公有成员（变量〡函数〡方法）
* 首字母小写：私有成员（变量〡函数〡方法）
* 对于多文件包注释只需要出现在任意其中一个文件前即可

### 公有私有函数
{% highlight java %}
package even
func Even(i int) bool { // 公有函数：首字母大写
	return i % 2 == 0
}
func odd(i int) bool { // 私有函数：首字母小写
	return i % 2 == 1
}
{% endhighlight %}

### 导入包
{% highlight java %}
package main
import (
	e "./even" // 相对路径方式导入用户库；用别名访问该包公有成员
	. "fmt" // 绝对路径方式导入标准库；可省略包名访问该包公有成员
	_ "github.com/mattn/go-sqlite3" // 绝对路径方式导入用户库；无法访问该包公有成员但会调用该包init函数
)
func main() {
	i := 5
	Printf("Is %d even? %v\n", i, e.Even(i))
}
{% endhighlight %}

