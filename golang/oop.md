---
layout: page
title: OOP
---

### JAVA代码
{% highlight java %}
// I.java
package org.oneslang.oop;
public interface I {
	int m(String s);
	int m(String s, String ss);
}

// P.java
package org.oneslang.oop.impl;
import org.oneslang.oop.I;
public class P implements I {
	public static String gs = ":global(static):";
	public int m(String s) {
		System.out.println(s);
		return 1;
	}
	public int m(String s, String ss) {
		System.out.println(s + ":" + ss);
		return 1;
	}
	public static void gf(String s, String ss) {
		System.out.println(s + gs + ss);
	}
}

// C.java
package org.oneslang.oop.impl;
public class C extends P {
	private String ps = "->private:exmaple";
	@Override
	public int m(String s) {
		pm(s);
		return 1;
	}
	private void pm(String s) {
		System.out.println(s + ps);
	}
}

// M.java
package org.oneslang.oop;
import org.oneslang.oop.impl.C;
import org.oneslang.oop.impl.P;
public class M {
	public static void main(String[] args) {
		I p = new P();
		p.m("P:public:example");      // output: P:public:example
		p.m("P:overload", "example"); // output: P:overload:example
		P.gf("P", "example");         // output: P:global(static):example
		I c = new C();
		c.m("C:public");              // output: C:public->private:exmaple
		c.m("C:overload", "example"); // output: C:overload:example
		C.gf("C", "example");         // output: C:global(static):example
	}
}
{% endhighlight %}

### Go代码
{% highlight java %}
// oop.go
package oop
import "fmt"
var gs string = ":global(static):"
func Gf(s, ss string) {
	fmt.Println(s + gs + ss)
}
type I interface {
	M(s string) int
	MM(s, ss string) int
}
type P struct{}
func (p *P) M(s string) int {
	fmt.Println(s)
	return 1
}
func (p *P) MM(s, ss string) int { // Go语言不支持函数重载
	fmt.Println(s + ":" + ss)
	return 1
}
type C struct {
	P
	ps string
}
func NewC() *C {
	return &C{ps: "->private:exmaple"}
}
func (c *C) M(s string) int {
	c.pm(s)
	return 1
}
func (c *C) pm(s string) {
	fmt.Println(s + c.ps)
}

// main.go
package main
import "./oop"
func main() {
	var p oop.I = new(oop.P)
	p.M("P:public:example")       // output: P:public:example
	p.MM("P:overload", "example") // output: P:overload:example
	oop.Gf("P", "example")        // output: P:global(static):example

	var c oop.I = oop.NewC()
	c.M("C:public:example")       // output: C:public->private:exmaple
	c.MM("C:overload", "example") // output: C:overload:example
	oop.Gf("C", "example")        // output: C:global(static):example
}
{% endhighlight %}

