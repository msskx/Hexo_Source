---
title: C++对象的初始化和清理
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++对象的初始化和清理
---

# 对象的初始化和清理

## 构造函数和析构函数

构造函数：主要作用在创建对象时为 对象成员属性赋值，构造函数由系统自动调用，无需手动调用

析构函数：主要作用在对象销毁前系统自动调用，执行一些清理工作。

### 构造函数语法  类名（）{}

1、构造函数，没有返回值，也不写void

2、函数名称与类名相同

3、构造函数可以有参数，因此可以发生重载

4、程序在创建对象时候会自动调用构造，无需手动调用，而且只会调用一次

### 析构函数语法 ~类名（）{}

1、析构函数，没有返回值也不写void

2、函数名称与类名相同，在名称前面加上符号**~**

3、析构函数不可以有参数，因此不可以发生重载

4、程序在对象销毁时会自动调用析构，无需手动调用而且只会调用一次

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	Person()
	{
		cout << "Person构造函数的调用" << endl;
	}
	~Person()
	{
		cout << "Person析构函数的调用" << endl;
	}
};
void test()
{
	Person p;//在栈上的数据，test（）执行完毕后，释放这个对象
}
int main() 
{
	test();
	return 0;
}
```

## 构造函数的分类及调用

### 分类

​	按参数分为：有参构造和无参构造

​	按类型分为：普通构造和拷贝构造

### 调用

​	括号法

​	显示法

​	隐式转换法

**实例**



```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	//按参数分为：有参构造和无参构造
	Person()
	{
		cout << "Person无参构造函数的调用" << endl;
	}
	Person(int a)
	{
		age = a;
		cout << "Person有参构造函数的调用" << endl;
	}
	//按类型分为：普通构造函数和拷贝构造函数
	//拷贝构造函数：将传入人身上所有的属性，拷贝到我身上
	Person(const Person &p)//传入的东西本身不能发生改变
	{
		age = p.age;
		cout << "Person拷贝构造函数的调用" << endl;
	}


	~Person()
	{
		cout << "Person析构函数的调用" << endl;
	}


	int age;
};
//调用方法
void test()
{
	//括号法
	Person p1;//默认构造函数的调用
	Person p2(4);//有参构造函数的调用
	Person p3(p2);//拷贝构造函数的调用将p2 的所有属性拷贝给p3
	//注意事项：不可以利用Person p1();调用默认构造函数否则编译器会认为是一个函数的申明而不是创建对象
	
	//显示法
	Person p4;//默认构造函数
	Person p5 = Person(4);//有参构造函数
	Person p6 = Person(p5);//拷贝构造函数
	//Person(4);匿名对象当前行结束后系统会立即回收匿名对象
	//不要利用拷贝构造函数初始化匿名对象，编译器会认为Person(p6)==Person p6;
	//隐式转换法
	Person p7 = 4;//相当于Person p7转换为Person P7(4);有参构造
	Person P8 = p7;//拷贝构造函数的隐式转换法

}
int main() 
{
	test();
	return 0;
}
```

## 拷贝构造函数的调用时机

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	
	Person()
	{
		cout << "Person无参构造函数的调用" << endl;
	}
	Person(int a)
	{
		age = a;
		cout << "Person有参构造函数的调用" << endl;
	}
	
	Person(const Person &p)
	{
		age = p.age;
		cout << "Person拷贝构造函数的调用" << endl;
	}


	~Person()
	{
		cout << "Person析构函数的调用" << endl;
	}


	int age;
};

void test01()
{
	//1、使用一个已经创建完毕的对象来初始化一个新对象
	Person p1(90);
	Person p2(p1);	
}
void Work01(Person p)
{

}
void test02()
{
	//2、以值传递的方式给函数参数传值
	Person p3;
	Work01(p3);

}
Person Work02()
{
	Person p ;
	return p;
}
void test03()
{	
	//3、值方式返回局部对象
	Person p3 = Work02();
}
int main() 
{
	test03();
	return 0;
}
```

## 构造函数调用规则

默认情况下，C++编译器至少给一个类添加3个函数

1、默认构造函数（无参，函数体为空）

2、默认析构函数（无参，函数体为空）

3、默认拷贝构造函数，对属性值进行拷贝

构造函数调用规则如下：
1、如果用户定义有参构造函数，C++不再提供默认无参构造，但是会提供默认拷贝构造

2、如果用户定义拷贝构造函数，C++不会再提供其他构造函数

​	

## 深拷贝与浅拷贝

#### 浅拷贝：简单的赋值拷贝操作

#### 深拷贝：在堆区重新申请空间，进行拷贝操作

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	
	Person()
	{
		
		cout << "Person默认构造函数的调用" << endl;
	}
	Person(int a,int height)
	{
		m_height = new int(height);
		age = a;
		cout << "Person有参构造函数的调用" << endl;
	}
	
	~Person()
	{
		if(m_height!=NULL)
		{
			delete m_height;//释放开辟的内存
			m_height = NULL;//防止野指针出现
		}
		cout << "Person析构函数的调用" << endl;
	}


	int age;
	int* m_height;
};

void test01()
{
	
	Person p1(9,150);
	cout << "P1的年龄为" << p1.age << "P1的身高为" <<*p1.m_height << endl;
	Person p2(p1);//编译器提供的拷贝构造函数，进行浅拷贝操作
	cout << "P2的年龄为" << p2.age << "P2的身高为" << *p2.m_height << endl;
}


int main() 
{
	test01();
	return 0;
}
```

**运行上述代码会出现以下情况**

![](https://img2020.cnblogs.com/blog/2279058/202103/2279058-20210328130454204-105989323.png)



**原因分析**

<u>浅拷贝导致堆区内存重复释放</u>

![](https://img2020.cnblogs.com/blog/2279058/202103/2279058-20210328130521110-426491792.png)


**解决方法**

自己进行深拷贝，避免内存的重复释放

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	
	Person()
	{
		
		cout << "Person默认构造函数的调用" << endl;
	}
	Person(int a,int height)
	{
		m_height = new int(height);
		age = a;
		cout << "Person有参构造函数的调用" << endl;
	}
	
	~Person()
	{
		if(m_height!=NULL)
		{
			delete m_height;//释放开辟的内存
			m_height = NULL;//防止野指针出现
		}
		cout << "Person析构函数的调用" << endl;
	}
	Person(const Person& p)
	{
		cout << "Person的拷贝构造函数调用" << endl;
		age = p.age;
		//m_height = p.m_height;
		//编译器默认提供的简单的赋值操作
		//自己写一个深拷贝解决问题
		m_height = new int(*p.m_height);//在堆区重新开辟一块内存，避免内存的重复释放
	}


	int age;
	int* m_height;
};

void test01()
{
	
	Person p1(9,150);
	cout << "P1的年龄为" << p1.age << "，P1的身高为" <<*p1.m_height << endl;
	Person p2(p1);//编译器提供的拷贝构造函数，进行浅拷贝操作
	cout << "P2的年龄为" << p2.age << "，P2的身高为" << *p2.m_height << endl;
}


int main() 
{
	test01();
	return 0;
}
```

## 初始化列表

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	
	//初始化列表初始化属性
	Person(int a, int b, int c) :m_a(a), m_b(b), m_c(c)
	{
			
	}
	int m_a;
	int m_b;
	int m_c;
};
void test01()
{
	
	Person p1(10,20,30);
	cout <<"A="<< p1.m_a << endl;
	cout << "B=" << p1.m_b << endl;
	cout << "C=" << p1.m_c << endl;
	
}
int main() 
{
	test01();
	return 0;
}
```

## 类对象作为类成员

C++中的成员可以是另一个类的对象，我们称该成员为**<u>对象成员</u>**

例如：

```cpp
class A {}
class B
{
	A a;
}
```

B类中有对象A作为成员，A为对象成员

**当其他类对象作为本类成员，构造时候先构造类对象，再构造自身**

**析构与构造相反**

```cppp
#include<iostream>
using namespace std;
#include<string>
class Phone
{
public:
	Phone(string Pname)
	{
		name = Pname;
		cout << "Phone构造" << endl;
	}
	~Phone()
	{
		cout << "Phone析构" << endl;
	}
	 
	string name;
};
class Person
{
public:
	Person(string name, string  Pname): m_name(name), p_name(Pname)
	{
		cout << "Person构造" << endl;
	}
	~Person()
	{
		cout << "Person析构" << endl;
	}
	string m_name;
	Phone p_name;
};
void test01()
{
	
	Person p1("张三","华为");
	cout << p1.m_name << "拿着：" << p1.p_name.name << endl;
}
int main() 
{
	test01();
	return 0;
}
```

##  静态成员

静态成员就是在成员变量和成员函数前加上关键词static，称为静态成员

### 静态成员分为：

	#### 	静态成员变量：

​	<u>所有对象共享同一份数据</u>

​	<u>在编译阶段分配内存</u>

​	<u>类内申明，类外初始化</u>

#### 静态成员函数：

​	<u>所有对象共享同一个函数</u>

​	<u>静态成员函数只能访问静态成员变量</u>

```cpp
#include<iostream>
using namespace std;
#include<string>
class Person
{
public:
	static void age()
	{
		//m_name = 89;
		m_age = 90;//静态成员函数只能访问静态成员变量
		cout << "Person静态成员函数的调用" << endl;
	}
	static int m_age;//类内定义
	int m_name;
private:
	static void name()
	{
		cout << "Person私有静态成员函数的调用" << endl;
	}
};
static int m_age = 9;//类外初始化
//有两种访问方式
void test01()
{
	//1，创建对象访问
	Person p;
	p.age();
	//2,通过类名访问
	Person::age();
	//Person::name();类外访问不到私有静态成员函数
	
}
int main() 
{
	test01();
	return 0;
}
```
