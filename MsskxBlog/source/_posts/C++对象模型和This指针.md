---
title: C++对象模型和This指针
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++对象模型和This指针笔记
---


# 对象模型和This指针

## 成员变量和成员函数分开储存

**在C++中成员变量和成员函数分开储存**

**只有非静态成员变量才属于类的对象上**

**静态成员函数，静态成员变量，非静态成员函数都不属于类对象上**

```cpp
#include<iostream>
using namespace std;
#include<string>
class Person
{
public:
	
	int m_age;
	static int m_name;
	 void func01()
	{

	}

};
static int m_age = 9;

void test01()
{
	
	Person p;
	cout << "sizeof:" << sizeof(p)<<endl;
	
}
int main() 
{
	test01();
	return 0;
}
```

## this指针概念

每一个非静态成员函数只会诞生一份函数实例，也就是说多个同类型的对象会共用一块代码

那么问题是：这一块代码是如何区分那个对象调用自己的呢？

c++通过提供特殊的对象指针，this指针，解决上述问题。

**this指针指向被调用的成员函数所属的对象**

this指针是隐含每一个非静态成员函数内的一种指针

this指针不需要定义，直接使用即可

this指针的用途：

- 当形参和成员变量同名时，可用this指针来区分
- 在类的非静态成员函数中返回对象本身，可使用return *this

```cpp
class Person
{
public:

	Person(int age)
	{
		//1、当形参和成员变量同名时，可用this指针来区分
		this->age = age;
	}

	Person& PersonAddPerson(Person p)
	{
		this->age += p.age;
		//返回对象本身
		return *this;
	}

	int age;
};

void test01()
{
	Person p1(10);
	cout << "p1.age = " << p1.age << endl;

	Person p2(10);
 //链式编程思想
	p2.PersonAddPerson(p1).PersonAddPerson(p1).PersonAddPerson(p1);
	cout << "p2.age = " << p2.age << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

#### 我在初次学习时还发现了这种情况

```cpp
#include<iostream>
using namespace std;
#include<string>
class Person
{
public:
	//1、解决名称冲突
	Person(int age)
	{
		this->age = age;
	}
	
	//2、返回对象本身
	Person* AddPerson(Person p)
	{
		this->age += p.age;
		//this指向p2本身，*this指向p2这个对象的本体
		return this;
	}

	int age;
};

void test01()
{
	
	Person p(10);
	Person p2(10);
	p2.AddPerson(p)->AddPerson(p)->AddPerson(p);
	cout << "p2的值为" << p2.age << endl;
	
}
int main() 
{
	test01();
	return 0;
}
```

##### 考虑其本质

**this指向p2本身，*this指向p2这个对象的本体**

**第一段代码返回*this是p的本体**

**链式调用的时候利用.来操作**

**第二段代码返回this是p指针**

**链式调用时用->来操作**

## 利用空指针访问成员函数



```cpp
#include<iostream>
using namespace std;
#include<string>
class Person
{
public:
	void ShowPerson()
	{
		cout << "this is Person" << endl;
	}
	void ShowAge()
	{
		cout << "this is Person'age" <<this->age<< endl;
	}

	int age;
};

void test01()
{
	Person* p;
	p = NULL;
	p->ShowAge();
	p->ShowPerson();

	 
	
}
int main() 
{
	test01();
	return 0;
}
```

**执行结果如下：**

 ![](https://img2020.cnblogs.com/blog/2279058/202103/2279058-20210328182320104-1181753326.png)



**//报错原因是传入this为NULL**

解决方法：判断后若为空直接return

```cpp
#include<iostream>
using namespace std;
#include<string>
class Person
{
public:
	void ShowPerson()
	{
		cout << "this is Person" << endl;
	}
	void ShowAge()
	{
		if (this == NULL)
		{
			return;
		}
		//报错原因是传入this为NULL
		cout << "this is Person'age" <<this->age<< endl;
	}

	int age;
};

void test01()
{
	Person* p;
	p = NULL;
	p->ShowAge();
	p->ShowPerson();

	 
	
}
int main() 
{
	test01();
	return 0;
}
```

## const 修饰成员函数

### 常函数：

成员函数后面加const后我们称这个函数为常函数

常函数不可以修饰成员属性

成员属性声明时加关键词mutable后在常函数中依然可以修改

### 常对象：

声明对象前加const称该对象为常对象

常对象只能调用常函数

```cpp
#include<iostream>
using namespace std;
#include<string>
class Person
{
public:
	
	void ShowAge()const
	{
		//this指针本质是指针常量Person *const this，指针指向是不可修改的
		//也不可修改其指向为空
		//在成员函数后面加const，修改的是this的指向，让指针指向的值也不可修改
		//const Person *const this
		//this->age = 89;
		this->year = 90;
		cout << "this is Person'year:" <<this->year<< endl;
	}
	void func()
	{
		age = 90;
	}
	int age;
	mutable int year;//特殊变量在常函数中也可以修改
};

void test01()
{
	Person p;
	
	p.ShowAge();
	
}
//常对象
void test02()
{
	const Person p1;
	//p.age = 90;
	p1.year = 90;//year是特殊值可以修改
	p1.ShowAge();//常对象只能调用常函数
	//p1.func();因为通过普通成员函数可以间接修改属性
}
int main() 
{
	test01();
	return 0;
}
```
