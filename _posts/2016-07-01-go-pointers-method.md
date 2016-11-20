---
title:  "Method,  interface and pointers in golang"
date:   Jul 7, 2016
categories: go, golang
published: true
---
- If a method is defined on a pointer to struct, the method can be called on a pointer to the struct type. In the example below, calling `ptr_s1.hello()` is fine since method `hello()` is defined on `*struct1`.

> [go play link](https://play.golang.org/p/sef4NPbNmR)

{% highlight go %}
type struct1 struct {
	greeting string
}

func (s *struct1) hello() {
	s.greeting = "hello"
}

func main() {
	ptr_s1 := &struct1{}
	fmt.Printf("ptr_s1 is of type : %+T\n", ptr_s1) // *main.struct1
	fmt.Printf("ptr_s1.greeting: %+v\n", ptr_s1)    // &{greeting:}

	ptr_s1.hello()
	fmt.Printf("ptr_s1.greeting: %+v\n", ptr_s1) // &{greeting:hello}

	s1 := struct1{}
	fmt.Printf("s1 is of type : %+T\n", s1) // main.struct1
	fmt.Printf("s1.greeting: %+v\n", s1)    // {greeting:}

	s1.hello()
	fmt.Printf("s1.greeting: %+v\n", s1) // {greeting:hello}
}
{% endhighlight %}

- However, method `hello()` is also callable on non pointer type `s1`. In fact, `struct1.greeting` gets populated with `hello`.
