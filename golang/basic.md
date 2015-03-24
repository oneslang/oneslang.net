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

### 变量
{% highlight go %}
package main

func main() {
	// 变量声明：
	var a1 string
	var b1 bool
	var c1 int
	var d1 float32
	println(a1, b1, c1, d1) // output:"" false 0 0.0

	// 变量声明赋值：
	var a2 string = "str2"
	var b2 bool = true
	var c2 int = 22
	var d2 float32 = 22.2
	println(a2, b2, c2, d2) // output:"str2" true 22 22.2

	// 变量类型推断：
	var a3 = "str3"
	var b3 = true
	var c3 = 33
	var d3 = 33.3
	println(a3, b3, c3, d3) // output:"str3" true 33 33.3

	// 简写方式（只可用在函数内）：
	a4 := "str4"
	b4 := true
	c4 := 44
	d4 := 44.4
	println(a4, b4, c4, d4) // output:"str4" true 44 44.4

	// 多个变量声明：
	var (
		a5            string
		b5            bool = true
		c5, c55, c555      = 5, 55, 555
		d5, d55       float32
	)
	println(a5, b5, c5, c55, c555, d5, d55) // output:"" true 5 55 555 0.0 0.0

	// 平行赋值：
	a, b := 10, true
	println(a, b) // output:10 true

	// 特殊的变量名：任何赋给它的值都被丢弃
	_, c := 15, 20
	println(c) // output:20
}
{% endhighlight %}

### 常量
{% highlight go %}
const ( // 常量只能是数字、字符串或布尔值
    a = 0
    b = 0.0
    c string = "0"
    d bool = false
)

const (
    a = "abc"  // a == "abc"
    b          // b == "abc" (可以省略重复的赋值)
    c = len(a) // c == 3 (常量值可以是len()、cap()、unsafe.Sizeof()常量计算表达式的值)
)

const (
    a = iota // a == 0 (iota在每个const开头都会被重设为0)
    b        // b == 1 (可以省略重复的赋值，当iota再次在新的一行使用时，它的值会增加1)
)

const (
    a = 1 << iota // a == 1
    b             // b == 2
    c             // c == 4
    d             // d == 8
    e = a | b     // e == 3
)
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
{% endhighlight %}

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

