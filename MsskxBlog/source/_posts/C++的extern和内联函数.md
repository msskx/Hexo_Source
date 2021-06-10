---
title: C++的extern和内联函数
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++的extern和内联函数的简单理解笔记
---

## 首先引入extern"C"的官方解释

extern "C" is meant to be recognized by a C++ compiler and to notify the compiler that the noted function is (or to be) compiled in C style.
Take an example, if you are working on a C++ project but it also deals with some existing C functions/libraries.
You want to wrap them in a C++ module or compile them with other C++ objects without any C++ compiler errors, then you would declare the C function prototypes in an extern "C" block to notify the compiler that they would be compiled along with other C++ functions into one module.
**翻译为汉语，大致为以下内容：**
extern“ C”旨在由C ++编译器识别，并通知编译器所注明的功能已（或将要）以C样式进行编译。
例如，如果您正在从事C ++项目，但它也处理一些现有的C函数/库。
您希望将它们包装在C ++模块中或与其他C ++对象一起编译而没有任何C ++编译器错误，然后在extern“ C”块中声明C函数原型以通知编译器它们将与其他C ++一起编译功能集成到一个模块中
通俗的来说，就是：
将C++里的代码用C语言的规则去编译。
来看官方给出的实例：

```cpp
my_C_CPP_Header.h://这是一个头文件（第三方库）

#ifndef MY_C_CPP_HEADER
#define MY_C_CPP_HEADER
/*check if the compiler is of C++*/检查编译器是否为C++
#ifdef __cplusplus
extern "C" {
int myOtherCfunc(int arg1, int arg2); /* a C function */
}
#endif

void myCppFunction1(); /* C++ function */
void myCppFunction2(); /* C++ function */

/*check if the compiler is of C++ */
#ifdef __cplusplus
}
#endif

#endif
```
我个人理解是：
首先检查是不是在C++编译器中执行C的代码，如果在C++编译器中而且是C的函数那么久将extern"C"里的代码编译为C的代码。
经过上述操作现在就可以将三个函数编译为一个模块。
**exturn"C"有两种书写方式**
**第一种**
```cpp
exturn "C"void func1();
exturn "C"void func2();
//exturn 后面的代码执行为C，以分号为结束
```
**第二种**

```cpp
exturn "C"{
void func1();
void func2();
}
//直接利用括号，那么exturn"C"的作用范围就是括号里的代码
```

原文摘自[C++官方](http://www.cplusplus.com/forum/general/1143/)

# C++内联函数

C++对代码有许多优化的地方，从某种程度上来看，内联函数就是一种优化，看一下C++官方标准对inline的描述：
*When the compiler inline-expands a function call, the function’s code gets inserted into the caller’s code stream (conceptually similar to what happens with a #define macro). This can, depending on a zillion other things, improve performance, because the optimizer can procedurally integrate the called code — optimize the called code into the caller.
There are several ways to designate that a function is inline, some of which involve the inline keyword, others do not. No matter how you designate a function as inline, it is a request that the compiler is allowed to ignore: the compiler might inline-expand some, all, or none of the places where you call a function designated as inline. (Don’t get discouraged if that seems hopelessly vague. The flexibility of the above is actually a huge advantage: it lets the compiler treat large functions differently from small ones, plus it lets the compiler generate code that is easy to debug if you select the right compiler options.)*
大致的意思就是：
**当编译器内联扩展函数调用时，该函数的代码将插入到调用者的代码流中（概念上与#define宏类似）。 取决于不计其数的其他方面，这可以提高性能，因为优化器可以在过程上集成被调用的代码—将被调用的代码优化到调用程序中。**
有几种方法可以指定一个函数为内联，其中一些涉及inline关键字，而其他则不涉及。 无论您如何将函数指定为内联函数，都要求编译器忽略该请求：编译器可能会内联扩展您调用被指定为内联函数的位置的部分，全部或全部。 （不要灰心，因为这似乎望尘莫及。上面的灵活性实际上是一个巨大的优势：它可以使编译器将大型函数与小型函数区别对待，另外，如果选择了，编译器可以生成易于调试的代码。 正确的编译器选项。）
通俗的来讲就是将函数的调用直接转为编程语句来执行，从而减少栈的操作。
来看下面的代码：

```cpp
inline int function（int a ,int b ){
return a + b;
}
int main(){
cout<<function(10,20)<<endl;
}
```
该程序执行时直接通过优化可近似看做：

```cpp
inline int function（int a ,int b ){
return a + b;
}
int main(){
cout<<10 + 20<<endl;
}
```

**内联函数会提高性能吗？**
没有简单的答案。内联函数可能会使代码变快，但可能会使代码变慢。它们可能使可执行文件变大，可能使可执行文件变小。它们可能会引起颠簸，它们可能会阻止颠簸。它们可能而且通常与速度完全无关。

原文摘自[C++官方](https://isocpp.org/wiki/faq/inline-functions#overview-inline-fns)