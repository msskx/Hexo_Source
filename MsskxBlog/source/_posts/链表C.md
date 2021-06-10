---
title: 链表C语言实现
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: 数据结构
categories: 数据结构
description: 链表的C语言实现
---

```c
#include<stdio.h>
#include<malloc.h>
#include<stdlib.h>
#include<stdbool.h>

typedef struct Node
{
	int data;
	struct Node* pNext;
}Node ,*pNode;
//创建节点类型
pNode create_SL();//创建单链表
void traverse(pNode pHead);//遍历链表
bool is_empty(pNode pHead);//判断是否为空
int get_len(pNode pHead);//求链表长度
void show_menu();//显示菜单
void insert(pNode pHead,int pos,int num);//在第pos个节点插入num
void delete(pNode pHead, int pos,int *val);//删除第pos个节点的元素
int main()
{
	pNode pHead = (pNode)malloc(sizeof(Node));
	
	while (true)
	{
		show_menu();
		printf("请输入要执行的操作");
		int select=0;
		scanf("%d", &select);
		switch (select)
		{
		case 1:
			pHead = create_SL();
			break;
		case 2:
			is_empty(pHead);
			break;
		case 3:
			printf("单链表的长度是%d", get_len(pHead));
			system("pause");
			system("cls");
			break;
		case 4:
			traverse(pHead);
			break;
		case 5:
		{
			if (is_empty(pHead))
			{
				system("cls");
				break;
			}
			printf("请输入要插入的位置\n");
			int pos;
			int num;
			scanf("%d", &pos);
			printf("请输入要插入的数字\n");
			scanf("%d", &num);
			insert(pHead, pos, num);
			break;
		}
		case 6:
		{
			printf("请输入要删除的位置\n");
			int pos;
			int* val;
			scanf("%d", &pos);
			delete(pHead,pos,&val);
			break;
		}

		default:
			printf("输入有误！程序终止");
			exit(-1);
			break;
		}
	}
	
	return 0;
}
pNode create_SL()//创建单链表头插法
{
	int len;//长度
	int val;//临时存放变量的值
	int i;//循环次数
	pNode pHead = (pNode)malloc(sizeof(Node));
	if (NULL == pHead)
	{
		printf("分配失败，程序终止！\n");
		exit(-1);
	}
	pHead->pNext = NULL;
	printf("请输入单链表的长度\n");
	scanf("%d", &len);
	for (i = 0; i < len; i++)
	{
		printf("请输入第%d个节点的值",i+1);
		scanf("%d", &val);
		pNode pNew = (pNode)malloc(sizeof(Node));
		if (NULL == pNew)
		{
			printf("分配失败，程序结束\n");
			exit(-1);
		}
		pNew->data = val;
		pNew->pNext=pHead->pNext;
		pHead->pNext = pNew;
	}
	printf("创建成功！");
	system("pause");
	system("cls");
	return pHead;
}
void traverse(pNode pHead)//遍历单链表
{
	pNode p = pHead->pNext;
	while (NULL !=p)
	{
		printf("%d\t", p->data);
		p = p->pNext;
	}
	printf("\n");
	system("pause");
	system("cls");
}
bool is_empty(pNode pHead)//判断是否为空
{
	if (pHead->pNext == NULL)
	{
		printf("单链表为空");
		return true;
	}
	else
	{
		printf("单链表不为空");
		return false;
	}
	system("pause");
	system("cls");
}
int get_len(pNode pHead)//求链表长度
{
	pNode p = pHead->pNext;
	int cnt = 0;
	while (NULL!=p)
	{
		cnt++;
		p = p->pNext;
	}
	//printf("单链表的长度为%d", cnt);
	system("pause");
	system("cls");
	return cnt;
}
void show_menu()
{
	printf("-----------------------------------------\n");
	printf("--------------非循环单链表---------------\n");
	printf("-----------------------------------------\n");
	printf("-------------1、创建单链表---------------\n");
	printf("-------------2、判断是否空---------------\n");
	printf("-------------3、显示表长度---------------\n");
	printf("-------------4、遍历单链表---------------\n");
	printf("-------------5、插入新节点---------------\n");
	printf("-------------6、删除废节点---------------\n");
	printf("-----------------------------------------\n");
	printf("-----------------------------------------\n");
	printf("-----------------------------------------\n");


}
void insert(pNode pHead, int pos, int num)//在第pos个节点插入num
{
	int i;
	pNode p = pHead->pNext;
	//判断是否可插入
	if (NULL == p)
	{
		printf("单链表为空！\n");
		printf("插入失败！\n");
		system("pause");
		system("cls");
		return;
	}
	else if (pos<0 || pos>get_len(pHead))
	{
		printf("无效的插入位置\n");
		printf("插入失败！\n");
		system("pause");
		system("cls");
		return;
	}
	else 
	{
		for (i = 0; i < pos; i++)
		{
			p = p->pNext;
		}
		pNode pNew = (pNode)malloc(sizeof(Node));
		pNew->data = num;
		pNew->pNext = p->pNext;
		p->pNext = pNew;
		printf("插入成功！");
		system("pause");
		system("cls");
		return;
	}
}
void delete(pNode pHead, int pos,int *val)//删除第pos个节点的元素并存在val 
{
	int i;
	pNode p = pHead;
	pNode temp;
	//判断是否可删除
	if (NULL == p)
	{
		printf("单链表为空！\n");
		printf("删除失败！\n");
		system("pause");
		system("cls");
		return;
	}
	else if (pos<0 || pos>get_len(pHead))
	{
		printf("无效的删除位置\n");
		printf("删除失败！\n");
		system("pause");
		system("cls");
		return;
	}
	else
	{
		for (i = 0; i < pos-1; i++)
		{
			p = p->pNext;
			*val = p->pNext->data;
		}
		p->pNext = p->pNext->pNext;
		temp = p->pNext;
		free(temp);
		printf("删除成功！\n");
		printf("删除的元素是%d", *val);
		system("pause");
		system("cls");
		return;
	}
}

```