---
layout: page
category: golang
name: basic
title: 基础
---

### 概念
* 不是`main`的其他包都被称为库
* 未显式初始化的变量都会被初始化为该类型的零值
* 变量声明赋值`:=`只可用在函数内
* 常量只能是数字、字符串或布尔值，可以使用`iota`生成枚举值
* 单个字符用单引号`'`，字符串用双引号`"`，多行字符用反引号`` ` ``
* 在Go中字符串是不可变的，一旦赋值就不能修改了
* 用`goto`跳转到一定是当前函数内定义的标签
* 数组长度是数组类型的一部分，因此不能改变数组长度，`[3]int`和`[5]int`是不同类型

### 关键字
{% highlight go %}
break    default      func    interface    select
case     defer        go      map          struct
chan     else         goto    package      switch
const    fallthrough  if      range        type
continue for          import  return       var
{% endhighlight %}

### 基本类型
* 字符串：string
* 布尔：bool
* 整数：int(int32〡int64), int8, int16, int32, int64
* 无符号整数：uint(uint32〡uint64), uint8, uint16, uint32, uint64, uintptr
* 字节：byte(uint8)
* 字符：rune(int32)
* 浮点：float32, float64
* 复数：complex64, complex128
* 错误：error

### 复合类型
* 指针：pointer
* 数组：array
* 切片：slice
* 映射：map
* 信道：chan
* 结构体：struct
* 接口：interface

### 零值
{% highlight go %}
string    ""
bool      false
*int*     0
float*    0.000000
complex*  0.000000+0.000000i
array     元素零值对应类型的零值
struct    元素零值对应类型的零值
// slice|map|chan:非零
// slice|map:通过make元素初始值对应类型的零值
// *int*:int,int8,int16,int32(rune),int64,uint,uint8(byte),uint16,uint32,uint64,uintptr
// float*:float32,float64
// complex*:complex64,complex128
{% endhighlight %}

### Hello World
{% highlight go %}
/*
 源代码必须以package <name>开头
 可执行文件必须是package main
*/
package main

// 将fmt包加入main，不是main的其他包都被称为库
import "fmt"

// 当Go程序在执行的时候，首先调用的函数是main.main()
func main() {
	// fmt包的函数打印字符串到屏幕
	fmt.Println("Hello, 世界") // output:Hello, 世界
}
{% endhighlight %}

### 变量
{% highlight go %}
package main

func main() {
	// 变量声明
	var s1 string
	var b1 bool
	var i1 int
	var f1 float32
	println(s1, b1, i1, f1) // output:"" false 0 0.0

	// 变量声明赋值
	var s2 string = "str2"
	var b2 bool = true
	var i2 int = 22
	var f2 float32 = 22.2
	println(s2, b2, i2, f2) // output:"str2" true 22 22.2

	// 变量类型推断
	var s3 = "str3"
	var b3 = true
	var i3 = 33
	var f3 = 33.3
	println(s3, b3, i3, f3) // output:"str3" true 33 33.3

	// 简写方式（只可用在函数内）
	s4 := "str4"
	b4 := true
	i4 := 44
	f4 := 44.4
	println(s4, b4, i4, f4) // output:"str4" true 44 44.4

	// 多个变量声明赋值
	var i5, i55, i555 = 5, 55, 555
	var (
		s5      string
		b5      bool = true		
		f5, f55 float32
	)
	println(i5, i55, i555, s5, b5, f5, f55) // output:5 55 555 "" true 0.0 0.0

	// 平行赋值
	i, b := 10, true
	println(a, b) // output:10 true

	// 特殊的变量名：任何赋给它的值都被丢弃
	_, c := 15, 20
	println(c) // output:20
}
{% endhighlight %}

### 常量
{% highlight go %}
package main

import "unsafe"

// 常量只能是数字、字符串或布尔值
const (
	i        = 0
	f        = 0.0
	s string = "0"
	b bool   = false
)

// 常量值还可以是len、cap、unsafe.Sizeof等编译期可确定结果的函数返回值
const (
	s1 = "abc"             // s1 == "abc"
	s2                     // s2 == "abc" (可以省略重复的赋值)
	i1 = len(s1)           // i1 == 3 (字符串长度)
	i2 = unsafe.Sizeof(s1) // i2 == 8 (数据所占用的字节数)
)

func main() {
	const c = "xxx" // 未使用局部常量不会引发编译错误
}
{% endhighlight %}

### 枚举
{% highlight go %}
package main

// 关键字iota定义常量组中从0开始按行计数的自增枚举值
const (
	Sunday    = iota // 0
	Monday           // 1，通常省略后续行表达式
	Tuesday          // 2
	Wednesday        // 3
	Thursday         // 4
	Friday           // 5
	Saturday         // 6
)

// 如果iota自增被打断，须显式恢复
const (
	A = iota // 0
	B        // 1
	C = "c"  // c
	D        // c，与上一行相同。
	E = iota // 4，显式恢复，注意计数包含了C、D两行
	F        // 5
)

const (
	a = 1 << iota // 1，左移位
	b             // 2
	c             // 4
	d             // 8
	e = a | b     // 3，按位或
)

// 在同一常量组中，可以提供多个iota，它们各自增长
const (
	AA, BB = iota, iota << 10 // 0, 0 << 10
	CC, DD                    // 1, 1 << 10
)

func main() {
	println(AA, BB, CC, DD) // output:0 0 1 1024
}
{% endhighlight %}

### string
{% highlight go %}
a := 'a'                // 单个字符
b := "abc"              // 字符串
c := `Starting part
			\r\n
      Ending part`      // 多行字符，不做转义处理

s := "Hello, World!"
s1 := s[0]                    // H
s2 := s[:5]                   // Hello
s3 := s[7:]                   // World!
s4 := s[1:5]                  // ello

package main
func main() {
    s := "abcd"
    bs := []byte(s)
    bs[1] = 'B'
    println(string(bs))    // output:aBcd
    u := "电脑"
    us := []rune(u)
    us[1] = '话'
    println(string(us))    // output:电话
}
{% endhighlight %}
### array
{% highlight go %}
var a [3]int
a := [3]int{1, 2, 3}
a := [...]int{1, 2, 3} // Go会自动统计元素的个数

a := [2][2]int{ [2]int{1,2}, [2]int{3,4} }
a := [2][2]int{ [...]int{1,2}, [...]int{3,4} }
a := [2][2]int{ {1,2}, {3,4} } // 元素复合声明的类型与外部一直时则可以省略
{% endhighlight %}

### slice
{% highlight go %}
sl := make([]int, 10)

a := [...]int{1, 2, 3, 4, 5}
s1 := a[2:4]
s2 := a[1:5]
s3 := a[:]
s4 := a[:4]
s5 := s2[:]

s0 := []int{0, 0}
s1 := append(s0, 2)
s2 := append(s1, 3, 5, 7)
s3 := append(s2, s0...)

var a = [...]int{0, 1, 2, 3, 4, 5, 6, 7}
var s = make([]int, 6)
n1 := copy(s, a[0:])   // n1 == 6, s == []int{0, 1, 2, 3, 4, 5}
n2 := copy(s, s[2:])   // n2 == 4, s == []int{2, 3, 4, 5, 4, 5}
l := len(n2)
c := cap(n2)
{% endhighlight %}

### map
{% highlight go %}
monthdays := map[string]int{
    "Jan": 31, "Feb": 28, "Mar": 31,
    "Apr": 30, "May": 31, "Jun": 30,
    "Jul": 31, "Aug": 31, "Sep": 30,
    "Oct": 31, "Nov": 30, "Dec": 31,   // 最后的逗号是必须的
}

year := 0
for _, days := range monthdays {
    year += days
}

monthdays["Undecim"] = 30 // 添加一个月
monthdays["Feb"] = 29     // 闰年时重写这个元素

v, ok := monthdays["Jan"] // 检查元素是否存在，如果存在ok值为true

delete(monthdays, "Mar")  // 删除元素
{% endhighlight %}

### if
{% highlight go %}
if x < 0 {
    return false
} else if x > 0 && x < 100 {
    return true
} else {
    return false
}

if err := file.Chmod(0664); err != nil {
    log.Stderr(err)
    return err
}
{% endhighlight %}

### goto
{% highlight go %}
func myfunc() {
    i := 0
Here:
    println(i)
    i++
    goto Here
}
{% endhighlight %}

### for
{% highlight go %}
sum := 0
for i := 0; i < 10; i++ {
	sum += i
}

for i, j := 0, len(a)-1; i < j; i, j = i+1, j-1 {
	a[i], a[j] = a[j], a[i]
}

J: for j := 0; j < 5; j++ {
	for i := 0; i < 10; i++ {
	    if i > 5 {
	        break J   // 现在终止的是变量j循环，而不是变量i的那个
	    }
	    println(i)
	}
}

for pos, char := range "ax" {
	fmt.Printf("character '%c' starts at byte position %d\n", char, pos)
}
{% endhighlight %}

### switch
{% highlight go %}
func unhex(c byte) byte {
    switch {
        case '0' <= c && c <= '9':
            return c - '0'
        case 'a' <= c && c <= 'f':
            return c - 'a' + 10
        case 'A' <= c && c <= 'F':
            return c - 'A' + 10
    }
    return 0
}

switch i {
    case 0:
    case 1: fallthrough
    case 2:
        println(i) // 当i==0时不会执行，i==1或2时会执行
    case 3,4,5,6:
        println(i) // 当i==4或5或6时执行
    default:
        println(i) // 当无符合条件时执行
}
{% endhighlight %}

