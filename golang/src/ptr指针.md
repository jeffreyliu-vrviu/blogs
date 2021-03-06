## 结论
### 一、【普通函数】
```go
func printFuncValue(p MyPoint) {} //参数是值  （值传递）
func printFuncPointer(pp *MyPoint) {} //参数是指针   （指针传递）
```
* 对于普通函数，参数【值】，则【只能传值】进去。        值传递， 【不改变】 结构内部数据。
* 对于普通函数，参数【指针】，则【只能传指针】进去。  指针传递， 会【改变】 结构内部数据。
### 二、【方法】
```go
func (p MyPoint) printMethodValue() {}  //接收者是值  （值传递）
func (p *MyPoint) printMethodPointer() {} //接收者是指针  （指针传递）
```
* 对于方法，接收者是值，    在使用时，【值和指针都可以】。   值传递， 【不改变】 结构内部数据。
* 对于方法，接收者是指针，  在使用时，【值和指针都可以】。 指针传递， 会【改变】 结构内部数据。

```go
type UU int

func (i UU) kaka1() int {
        i = i + 1  // 仅在内部改变 ， 值传递
        x := i + 1
        return int(x)
}
func (i *UU) kaka() int {
        *i = *i + 1  // 改变了 *i， 外部也改变， 指针传递
        m := *i
        m = m + 1
        x := int(m)
        return x
}
```
* 调用方法如下：t1=&t0,  t0.kaka() 和 t1.kaka()一样,   t0.kaka1() 和 t1.kaka1()一样
* kaka(), 指针传递，会改变数据，  kaka1()是值传递， 不改变数据。
```go
        var t0 UU
        t0 = 6
        var y0 int
        t1 := &t0
        y0 = t0.kaka()
        y0 = t0.kaka()
        y0 = t0.kaka()
        y0 = t0.kaka()
        fmt.Printf("after point zz --> %v\n", t0)
        fmt.Printf("after point zz --> %v\n", y0)
        y0 = t1.kaka()
        y0 = t1.kaka()
        y0 = t1.kaka()
        y0 = t1.kaka()
        fmt.Printf("after point t1.kaka() --> %v\n", t0)
        fmt.Printf("after point t1.kaka() --> %v\n", y0)
        y0 = t0.kaka1()
        y0 = t0.kaka1()
        y0 = t0.kaka1()
        y0 = t0.kaka1()
        fmt.Printf("after point zz --> %v\n", t0)
        fmt.Printf("after point zz --> %v\n", y0)
        y0 = t1.kaka1()
        y0 = t1.kaka1()
        y0 = t1.kaka1()
        y0 = t1.kaka1()
        fmt.Printf("after point t1.kaka1() --> %v\n", t0)
        fmt.Printf("after point t1.kaka1() --> %v\n", y0)

```

***

```go
[GD-0103-0121@rjsys ~/go/src/ptr]$
[GD-0103-0121@rjsys ~/go/src/ptr]$ cat a.go
package main

import "fmt"

type MyPoint struct {
        X int
        Y int
}

func printFuncValue(p MyPoint) {
        p.X = 1
        p.Y = 1
        fmt.Printf(" -> %v", p)
}

func printFuncPointer(pp *MyPoint) {
        pp.X = 1 // 实际上应该写做 (*pp).X，Golang 给了语法糖，减少了麻烦，但是也导致了 * 的不一致
        pp.Y = 1
        fmt.Printf(" -> %v", pp)
}

func (p MyPoint) printMethodValue() {
        p.X += 1
        p.Y += 1
        fmt.Printf(" -> %v", p)
}

// 建议使用指针作为方法（method：printMethodPointer）的接收者（receiver：*MyPoint），一是可以修改接收者的值，二是可以避免大对象的复制
func (p *MyPoint) printMethodPointer() {
        p.X += 1
        p.Y += 1
        fmt.Printf(" -> %v", p)
}

/*
func (i int) kaka1() int {
        x := i + 1
        return int(x)
}
*/

type UU int

func (i UU) kaka1() int {
        i = i + 1
        x := i + 1
        return int(x)
}
func (i *UU) kaka() int {
        *i = *i + 1
        m := *i
        m = m + 1
        x := int(m)
        return x
}

func main() {
        p := MyPoint{0, 0}
        pp := &MyPoint{0, 0}

        fmt.Printf("\n value to func(value): %v", p)
        printFuncValue(p)
        fmt.Printf(" --> %v", p)
        // Output: value to func(value): {0 0} -> {1 1} --> {0 0}
        //printFuncValue(pp) // cannot use pp (type *MyPoint) as type MyPoint in argument to printFuncValue
        //printFuncPointer(p) // cannot use p (type MyPoint) as type *MyPoint in argument to printFuncPointer

        fmt.Printf("\n pointer to func(pointer): %v", pp)
        printFuncPointer(pp)
        fmt.Printf(" --> %v", pp)
        // Output: pointer to func(pointer): &{0 0} -> &{1 1} --> &{1 1}

        fmt.Printf("\n value to method(value): %v", p)
        p.printMethodValue()
        fmt.Printf(" --> %v", p)
        // Output: value to method(value): {0 0} -> {1 1} --> {0 0}

        fmt.Printf("\n value to method(pointer): %v", p)
        p.printMethodPointer()
        fmt.Printf(" --> %v", p)
        // Output: value to method(pointer): {0 0} -> &{1 1} --> {1 1}

        fmt.Printf("\n pointer to method(value): %v", pp)
        pp.printMethodValue()
        fmt.Printf(" --> %v", pp)
        // Output: pointer to method(value): &{1 1} -> {2 2} --> &{1 1}

        fmt.Printf("\n pointer to method(pointer): %v", pp)
        pp.printMethodPointer()
        fmt.Printf(" --> %v", pp)
        // Output: pointer to method(pointer): &{1 1} -> &{2 2} --> &{2 2}

        p = MyPoint{0, 0}
        yy := p
        zz := &yy

        fmt.Println(" ")
        fmt.Printf(" yy --> %v\n", yy)
        fmt.Printf(" zz --> %v\n", zz)
        yy.printMethodValue()
        yy.printMethodValue()
        yy.printMethodValue()
        yy.printMethodValue()
        fmt.Println(" ")
        zz.printMethodValue()
        zz.printMethodValue()
        zz.printMethodValue()
        zz.printMethodValue()
        zz.printMethodValue()
        zz.printMethodValue()
        zz.printMethodValue()
        fmt.Println(" ")
        fmt.Printf("after value yy --> %v\n", yy)
        fmt.Printf("after value zz --> %v\n", zz)
        fmt.Println(" ")
        fmt.Printf(" yy --> %v\n", yy)
        fmt.Printf(" zz --> %v\n", zz)
        yy.printMethodPointer()
        yy.printMethodPointer()
        yy.printMethodPointer()
        yy.printMethodPointer()
        fmt.Println(" ")
        fmt.Printf(" yy --> %v\n", yy)
        zz.printMethodPointer()
        fmt.Println(" ")
        fmt.Printf("after point yy --> %v\n", yy)
        fmt.Printf("after point zz --> %v\n", zz)
        fmt.Println(" ")

        var t0 UU
        t0 = 6
        var y0 int
        t1 := &t0
        y0 = t0.kaka()
        y0 = t0.kaka()
        y0 = t0.kaka()
        y0 = t0.kaka()
        fmt.Printf("after point zz --> %v\n", t0)
        fmt.Printf("after point zz --> %v\n", y0)
        y0 = t1.kaka()
        y0 = t1.kaka()
        y0 = t1.kaka()
        y0 = t1.kaka()
        fmt.Printf("after point t1.kaka() --> %v\n", t0)
        fmt.Printf("after point t1.kaka() --> %v\n", y0)
        y0 = t0.kaka1()
        y0 = t0.kaka1()
        y0 = t0.kaka1()
        y0 = t0.kaka1()
        fmt.Printf("after point zz --> %v\n", t0)
        fmt.Printf("after point zz --> %v\n", y0)
        y0 = t1.kaka1()
        y0 = t1.kaka1()
        y0 = t1.kaka1()
        y0 = t1.kaka1()
        fmt.Printf("after point t1.kaka1() --> %v\n", t0)
        fmt.Printf("after point t1.kaka1() --> %v\n", y0)

}
[GD-0103-0121@rjsys ~/go/src/ptr]$ ./ptr.exe

 value to func(value): {0 0} -> {1 1} --> {0 0}
 pointer to func(pointer): &{0 0} -> &{1 1} --> &{1 1}
 value to method(value): {0 0} -> {1 1} --> {0 0}
 value to method(pointer): {0 0} -> &{1 1} --> {1 1}
 pointer to method(value): &{1 1} -> {2 2} --> &{1 1}
 pointer to method(pointer): &{1 1} -> &{2 2} --> &{2 2}
 yy --> {0 0}
 zz --> &{0 0}
 -> {1 1} -> {1 1} -> {1 1} -> {1 1}
 -> {1 1} -> {1 1} -> {1 1} -> {1 1} -> {1 1} -> {1 1} -> {1 1}
after value yy --> {0 0}
after value zz --> &{0 0}

 yy --> {0 0}
 zz --> &{0 0}
 -> &{1 1} -> &{2 2} -> &{3 3} -> &{4 4}
 yy --> {4 4}
 -> &{5 5}
after point yy --> {5 5}
after point zz --> &{5 5}

after point zz --> 10
after point zz --> 11
after point t1.kaka() --> 14
after point t1.kaka() --> 15
after point zz --> 14
after point zz --> 16
after point t1.kaka1() --> 14
after point t1.kaka1() --> 16
[GD-0103-0121@rjsys ~/go/src/ptr]$

```
