---
title: 运算符重载
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++运算符重载
---

# 加号运算符重载

对于内置数据类型，编译器知道如何运算

但是对于自己封装的类，编译器无法进行运算

这时可以通过自己定义运算符重载进行运算

**<u>operator+</u>**

## 通过成员函数重载+号

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	int m_a;
	int m_b;
	//通过成员函数实现重载
	Person operator+ (Person &p)
	{
		//创建一个临时变量
		Person temp;
		temp.m_a = this->m_a + p.m_a;
		temp.m_b = this->m_b + p.m_b;
		return temp;
	}
};
void test01()
{
	Person p1;
	p1.m_a = 66;
	p1.m_b = 44;
	Person p2;
	p2.m_a = 6;
	p2.m_b = 4;
	Person p3;
	//通过函数原型调用
	p3 = p1.operator+(p2);
	//简便调用
	//p3 = p1 + p2;
	cout << "p3.m_a:" << p3.m_a << endl;
	cout << "p3.m_b:" << p3.m_b << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

**注意两种调用方式**

**通过函数原型调用**
	**p3 = p1.operator+(p2);**
**简便调用**
	**p3 = p1 + p2;**

## 通过全局函数重载+号

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	int m_a;
	int m_b;
};
//通过全局函数实现重载
Person operator+ (Person& p1, Person& p2)
{
	//创建一个临时变量
	Person temp;
	temp.m_a = p1.m_a + p2.m_a;
	temp.m_b = p1.m_b + p2.m_b;
	return temp;
}
void test01()
{
	Person p1;
	p1.m_a = 66;
	p1.m_b = 44;
	Person p2;
	p2.m_a = 6;
	p2.m_b = 4;
	Person p3;
	//函数原型调用
	p3 = operator+(p1,p2);
	//简便调用
	//p3 = p1 + p2;
	cout << "p3.m_a:" << p3.m_a << endl;
	cout << "p3.m_b:" << p3.m_b << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

**注意两种调用方式**

**通过函数原型调用**
	**p3 = operator+(p1,p2);**
**简便调用**
	**p3 = p1 + p2;**

## 运算符重载发生函数重载

运算符重载可以发生函数重载：Person+int等等

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	int m_a;
	int m_b;
};
//通过全局函数实现重载
Person operator+ (Person& p1, int num)
{
	//创建一个临时变量
	Person temp;
	temp.m_a = p1.m_a + num;
	temp.m_b = p1.m_b + num;
	return temp;
}
void test01()
{
	Person p1;
	p1.m_a = 66;
	p1.m_b = 44;
	Person p2;
	p2.m_a = 6;
	p2.m_b = 4;
	Person p3;
	//函数原型调用
	//p3 = operator+(p1,55);
	//简便调用
	p3 = p1 + 55;
	cout << "p3.m_a:" << p3.m_a << endl;
	cout << "p3.m_b:" << p3.m_b << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

调用方法和定义方法与上面相同，不再多余赘述

## 总结

1、系统内置数据类型的表达式不可改变

2、不要滥用运算符重载

# 左移运算符

不利用成员函数重载左移运算符

没有具体演示，因为报错，我也没写出来

### 下面通过全局函数实现

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	int m_a;
	int m_b;
	
};
ostream& operator<<(ostream& cout,Person&p)
{
	cout << "p.m_a=" <<p. m_a << "  p.m_b=" <<p. m_b << endl;
	return cout;
}
void test01()
{
	Person p1;
	p1.m_a = 44;
	p1.m_b = 66;
	cout << p1 << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

因为要实现链式，实现追加，所以返回值必须是ostream

## 总结

配合友元实现自定义输出类型

# 递增运算符重载

## 递增运算符重载

```cpp
#include<iostream>
using namespace std;
class myInt
{
	friend ostream& operator<<(ostream& cout, myInt num);
public:
	myInt()
	{
		this->m_a = 0;
	}
	//前置++运算符重载
	myInt& operator++()//返回引用是为了一直对一个数据进行递增，否则函数默认返回一个新的数
	{
		//先进行++
		m_a++;
		//然后返回自身
		return *this;
	}
	//后置++运算符重载
	myInt operator++(int)//int表示占位参数，用于区分前置后置参数
	{
		//先记录当前的值
		myInt temp=*this;
		//再递增
		m_a++;
		//然后返回记录的值
		return  temp;
	}
private:
	int m_a;	
};
//左移运算符重载
ostream& operator<<(ostream& cout, myInt num)
{
	cout << num.m_a;
	return cout;
}
void test01()
{
	myInt myint;
	cout << myint << endl;
	cout << ++myint << endl;
	cout << myint << endl;

}
int main()
{
	test01();
	system("pause");
	return 0;
}
```



# 赋值运算符重载

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	Person(int num)//将数据开辟到堆区
	{
		m_a = new int(num);
	}
	~Person()
	{
		if (m_a != NULL)
		{
			delete m_a;
			m_a = NULL;
		}
	}
	//重载赋值运算符
	Person& operator=(Person &p)//返回值用Person返回本身，可执行连等
	{
		//先判断是否有属性在堆区，如果有先释放干净
		if (m_a != NULL)
		{
			delete m_a;
			m_a = NULL;
		}
		m_a = new int(*p.m_a);
		return *this;
	}
	int* m_a;
	
};
void test01()
{
	Person p1(18);
	Person p2(209);
	Person p3(9);
	p2 = p1 = p3;
	cout << *p1.m_a << endl;
	cout << *p2.m_a << endl;
	cout << *p3.m_a << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

# 关系运算符重载

```cpp
#include<iostream>
using namespace std;
#include<string>
class Person
{
public:
	
	Person(string name, int age)
	{
		this->age = age;
		this->name = name;
	}
	bool operator==(Person& p)
	{
		if (this->age == p.age && this->name == p.name)
		{
			return true;
		}
		else {
			return false;
		}
	}
	bool operator!=(Person& p)
	{
		if (this->age == p.age && this->name == p.name)
		{
			return false;
		}
		else {
			return true;
		}
	}
	string name;
	int age;

	
};
void test01()
{
	Person p1("gouride", 19);
	Person p2("gouride", 19);
	if (p1 == p2) {
		cout << "p1和p2相同" << endl;
	}
	else {
		cout << "p1和p2不相同" << endl;
	}
	if (p1 != p2) {
		cout << "p1和p2不相同" << endl;
	}
	else {
		cout << "p1和p2相同" << endl;
	}
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

# 函数调用重载

仿函数

```cpp
#include<iostream>
using namespace std;
#include<string>
class Myprint
{
public:
	void operator()(string name)
	{
		cout << name << endl;
	}
	int operator()(int a,int b)
	{
		return a + b;
	}
};
void test01()
{
	
	Myprint myprint;
	myprint("测试");
	//匿名对象调用
	cout << Myprint()(4,6) << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

