---
title: C++实现控制台计算器
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++控制台计算器
---

*没什么好解释的*
**直接创建一个父类：计算类**
**定义好运算的数字以及运算方式，子类继承父类，父类创建纯虚函数，子类重写父类的纯虚函数**
**我添加了一个简易的菜单，以及控制台美化**
**请按照测试图的测试方法进行输入测试**
```cpp
#include<iostream>
using namespace std;
#include<string>
#include<Windows.h>
class calculator
{
public:
	virtual int getresult()
	{
		return 0;
	}
	int num1=0;
	int num2=0;
};//创建一个计算器基类
class Add:public calculator 
{
public:
	int getresult()
	{
		return num1+num2;
	}
};//加法
class Sub :public calculator
{
public:
	int getresult()
	{
		return num1 - num2;
	}
};//减法
class Mul :public calculator
{
public:
	int getresult()
	{
		return num1 * num2;
	}
};//乘法
class Chu :public calculator
{
public:
	int getresult()
	{
		return num1 / num2;
	}
};//除法
void cacunlate(int num1,int num2,char ch)
{
	if (ch == '+')
	{
		calculator* abc = new Add;
		abc->num1 = num1;
		abc->num2 = num2;
		cout << abc->num1 << ch << abc->num2 << "=" << abc->getresult() << endl;
	}
	else if (ch == '-')
	{
		calculator* abc = new Sub;
		abc->num1 = num1;
		abc->num2 = num2;
		cout << abc->num1 << ch << abc->num2 << "=" << abc->getresult() << endl;
	}
	else if (ch == '*')
	{
		calculator* abc = new Mul;
		abc->num1 = num1;
		abc->num2 = num2;
		cout << abc->num1 << ch << abc->num2 << "=" << abc->getresult() << endl;
	}
	else if (ch == '/')
	{
		calculator* abc = new Chu;
		abc->num1 = num1;
		abc->num2 = num2;
		cout << abc->num1 << ch << abc->num2 << "=" << abc->getresult() << endl;
	}
	else
	{
		cout << "错误！！" << endl;
	}

}//计算
void menu(int num1, int num2, char ch)
{
	cout << "请输入要计算的算式：（回车代表每一阶段结束）" << endl;
	cin >> num1;
	cin >> ch;
	cin >> num2;
	cout << "您要计算的算式是：" << endl;
	cacunlate(num1, num2, ch);
	system("pause");
	system("cls");
}//菜单函数
int main()
{
	system("color B1");//美化控制台
	int num1 = 0;
	int num2 = 0;
	char ch = '+';
	while (1)
	{
		cout << "欢迎使用辣鸡计算器" << endl;
TEMP:	cout << "请选择功能：" << endl;
		cout << "1、计算" << endl;
		cout << "2、退出" << endl;
		int select;
			cin >> select;
			if (select == 1)
			{
				menu(num1, num2, ch);
			}
			else if (select == 2)
			{
				cout << "欢迎下次使用" << endl;
				system("pause");
				exit(-1);
			}
			else
			{
				cout << "输入有误" << endl;
				system("pause");
				system("cls");
				goto TEMP;
			}
	}
	system("pause");
	return 0;
}
```
