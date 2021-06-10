---
title: typedef的使用
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++/C的typedef的使用笔记
---

## 1、初级

```cpp
#include <stdio.h>


//首先定义一个结构体变量student
typedef struct student
{
    int age;
    double heigth;
    int number;
}STU;//相当于再给student这个结构体取一个名字
int main()
{
    STU mashuai;
    mashuai.age = 100;//使用这个结构体变量时，直接用一个点
    printf("%d\n", mashuai.age);
    return 0;
}


```

## 2、中级

```cpp
#include <stdio.h>
//首先定义一个结构体变量student
typedef struct student
{
    int age;
    double heigth;
    int number;
}*PSTU;//相当于再给student这个结构体取一个指针类型的名字，
//等价于struct student*一般指针类型前面加一个P
int main()
{
    struct student mashuai;//创建一个结构体变量
    PSTU ms = &mashuai;//用一个同类型的指针变量去接收
    ms->age = 100;//使用这个结构体变量和利用结构体内的指针一样，用->
    printf("%d\n", ms->age);
    return 0;
}


```

## 3、高级

```cpp
#include <stdio.h>
//首先定义一个结构体变量student
typedef struct student
{
    int age;
    double heigth;
    int number;
}*PSTU ,STU;
//*PSTU等价于struct student*    (结构体指针)
// STU相当于  struct student    (结构体本身)
//
int main()
{
    STU mashuai;//创建一个结构体变量
    PSTU ms = &mashuai;//用一个同类型的指针变量去接收
    ms->age = 100;//使用这个结构体变量和利用结构体内的指针一样，用->
    printf("%d\n", ms->age);
    return 0;
}


```

**<u>个人笔记，如有错误欢迎指正</u>**
