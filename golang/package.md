---
layout: page
category: golang
name: package
title: 包
---

### 概念
* 包是函数和数据的集合
* 包可以由多个文件组成
* 文件名不需要与包名一致
* 目录名不需要与包名一致（访问公有或私有成员是通过包名而不是通过目录名）
* 一个目录只能对应一个包名（除了main和*_test包名）
* 包名用的是根目录名：在src/pkg/compress/gzip的包，作为compress/gzip导入，但名字是gzip
* 首字母大写：公有成员（变量〡函数〡方法）
* 首字母小写：私有成员（变量〡函数〡方法）
* 紧挨着包语句前面的块注释就是包注释，包语句前面隔了空行的块注释不是包注释
* 对于多文件的包的包注释只需要出现在任意其中一个文件中即可，通常包注释放在单独文件`doc.go`中

### 公有私有函数
{% highlight go %}
package even
func Even(i int) bool { // 公有函数：首字母大写
	return i % 2 == 0
}
func odd(i int) bool { // 私有函数：首字母小写
	return i % 2 == 1
}
{% endhighlight %}

### 导入包
{% highlight go %}
package main
import (
	e "./even"                      // 相对路径方式导入用户库；用别名访问该包公有成员
	. "fmt"                         // 绝对路径方式导入标准库；可省略包名访问该包公有成员
	_ "github.com/mattn/go-ole"     // 绝对路径方式导入用户库；无法访问该包公有成员但会调用该包init函数
	_ "github.com/mattn/go-sqlite3" // "github.com/mattn/go-sqlite3"是路径，和包名无关，包名通过“package sqlite3”指定
)
func main() {
	i := 5
	Printf("%d is even? %t\n", i, e.Even(i))
}
{% endhighlight %}
