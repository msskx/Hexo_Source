---
title: C语言实现栈
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: 数据结构
categories: 数据结构
description: 栈的基本实现C语言
---

# 栈(先进后出)

**定义：**

一种可以实现“先进后出”数据存储结构，通俗的理解就是：**我把东西吃进去再吐出来**

也类似于腌酸菜，一口大缸，放入菜后先放进去的酸菜只能最后取出来

一般的：表尾叫栈顶，表头叫栈底

**分类：**

静态栈：

动态栈：

**算法：**

入栈/压栈、出栈、遍历

**应用：**

函数调用、终端、数制转换、表达式求值、内存分配、缓冲处理、迷宫、括号匹配性检验、行编辑程序

**下面简单实现栈的基本功能**

（链式栈和顺序栈）

```cpp
//链式栈的实现
#include<iostream>
#include<malloc.h>
#include<stdlib.h>
typedef struct Node
{
	int data;
	Node* pNext;
}NODE,*PNODE;
typedef struct Stack
{
	PNODE pTop;
	PNODE pBottom;
}STACK, * PSTACK;

void init(PSTACK);//初始化
void push(PSTACK, int);//压栈
bool empty(PSTACK);//判断栈是否空
void traverse(PSTACK);//遍历
void pop(PSTACK, int*);//出栈并保留元素
void clear(PSTACK);//清空
int main()
{
	STACK S;//定义一个栈
	int val;//出栈临时数字
	init(&S);//初始化一个栈
	push(&S, 1);//把1压进去
	push(&S, 2);//把2压进去
	push(&S, 3);//把3压进去
	push(&S, 4);//把4压进去
	push(&S, 5);//把5压进去
	traverse(&S);//遍历
	pop(&S, &val);//把5吐进去
	clear(&S);//清空栈内所有元素，使之为空栈
	empty(&S);//判断一下是否为空
}
void init(PSTACK pS)
{
	pS->pTop = (PNODE)malloc(sizeof(NODE));
	if (NULL == pS->pTop)
	{
		printf("初始化失败！！\n");
		exit(-1);
	}
	else
	{
		pS->pBottom = pS->pTop;
		pS->pTop->pNext = NULL;
	}
}
void push(PSTACK pS, int val)
{
	PNODE pNew = (PNODE)malloc(sizeof(NODE));
	if (NULL == pNew)
	{
		printf("入栈失败！！\n");
		exit(-1);
	}
	else
	{
		pNew->data = val;
		pNew->pNext = pS->pTop;
		pS->pTop = pNew;
	}
}
void traverse(PSTACK pS)
{
	PNODE p = pS->pTop;
	while (p != pS->pBottom)
	{
		printf("%d  ", p->data);
		p = p->pNext;
	}
	printf("\n");
}
bool empty(PSTACK pS)
{
	if (pS->pTop == pS->pBottom)
	{
		printf("空栈一个！！\n");
		return true;
	}
	else
	{
		printf("不是空栈！！\n");
		return false;
	}
}
void pop(PSTACK pS, int *val)
{
	if (empty(pS)==true)
	{
		printf("出栈失败，该栈为空！！\n");
	}
	else
	{
		PNODE p = pS->pTop;
		*val = p->data;
		pS->pTop = p->pNext;
		free(p);
		p = NULL;
		printf(" 出栈成功，删除的元素是%d \n", *val);
	}
}
void clear(PSTACK pS)
{
	PNODE p, q;
	p = pS->pTop;
	q = p->pNext;
	while (NULL != p)
	{
		q = p->pNext;
		free(p);
		p = q;
	}
	pS->pTop = pS->pBottom;
	printf("该栈已被清空！\n");
}
```



```cpp
//顺序栈的实现
#include <stdio.h>
#include<malloc.h>
#include<stdlib.h>
typedef struct Stack
{
    int len;//栈大小
    int* data;//
    int top;//存放栈顶元素下标
}STACK,*PSTACK;
void init(PSTACK,int);//把栈和栈的大小传进去
bool isempty(PSTACK);//判断空
bool isfull(PSTACK);//判断满
void push(PSTACK,int);//压栈操作
void pop(PSTACK,int*);//出栈操作,保存出栈的元素
void traverse(PSTACK);//遍历栈中元素
int main()
{
    STACK stack;
   /* 
   可以手动输入栈的大小
   printf("请输入栈的大小：\n");
    int n;
    scanf_s("%d", &n);
    */
    init(&stack, 5);//初始化一个大小为5的栈
    push(&stack, 1);//将1压入栈中
    push(&stack, 2);//将2压入栈中
    push(&stack, 3);//将3压入栈中
    push(&stack, 4);//将4压入栈中
    push(&stack, 5);//将5压入栈中
    traverse(&stack);//遍历一下
    int* val = (int *)malloc(sizeof(int));//为保存出栈的数据创建一块临时空间
    pop(&stack,val);//出栈
    pop(&stack, val);//出栈
    traverse(&stack);//遍历
    return 0;
}
void init(PSTACK S,int len)
{
    S->data = (int*)malloc(sizeof(int) * len);
    if (NULL == S->data)
    {
        printf("初始化失败！！！\n");
        exit(-1);
    }
    else
    {
        S->top = -1;
        S->len = len;
    }
}
bool isempty(PSTACK S)
{
    if (S->top == -1)
        return true;
    else
        return false;
}
bool isfull(PSTACK S)
{
    if (S->top == S->len - 1)
        return true;
    else
        return false;
}
void push(PSTACK S,int val)
{
    if (isfull(S))
    {
        printf("该栈已满，无法继续操作\n");
        return;
    }
    else
    {
        S->top++;
        S->data[S->top] = val;
        return;
    }
}
void pop(PSTACK S,int *val)
{
    if (isempty(S))
    {
        printf("该栈为空，无法出栈！！\n");
        return;
    }
    else
    {
        *val = S->data[S->top];
        S->top--;
        printf("出栈成功，出栈的元素是%d \n", *val);
        return;
    }
}
void traverse(PSTACK S)
{
    if (isempty(S))
    {
        printf("该栈为空，无法输出\n");
        return;
    }
    else
    {
        int i;
        for (i = 0; i < S->top+1; i++)
        {
            printf("%d  ", S->data[i]);
        }
        printf("\n");
    }
}
```

