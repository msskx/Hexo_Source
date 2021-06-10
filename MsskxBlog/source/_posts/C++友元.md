---
title: 友元
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++的友元
---

# 友元

情景导入：

在家里，有客厅（public），也有卧室（private）

客厅可以每个人都进来，可是卧室是私有的，只有我能进入

但是经过允许也有人可以进入

在程序中，有些私有的属性也想让类外特殊的一些函数或者类访问，就需要用到友元技术

友元的目的就是让函数或者类访问一个类中的私有成员

友元的关键字为

```cpp
friend
```



## 全局函数做友元

```cpp
#include<iostream>
using namespace std;
#include<string>
class Home
{
	friend void see(Home* home);//将全局函数变成“好朋友”就可以访问私有属性
public:
	Home()
	{
		m_livingroom = "客厅";
		m_bedroom = "卧室";

	}
	string m_livingroom;//客厅
private:
	string m_bedroom;//卧室
};
void see(Home *home)
{
	cout << "好朋友正在参观你的" << home->m_livingroom << endl;
	cout << "好朋友正在参观你的" << home->m_bedroom << endl;
}
void test01()
{
	Home horse;
	see(&horse);
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

## 类做友元

``` cpp
#include<iostream>
using namespace std;
#include<string>

class Home
{
	friend class Goodfriend;
public:
	//Home构造函数
	Home()
	{
		this->m_livingroom = "客厅";
		this->m_bedroom = "卧室";

	}
	string m_livingroom;//客厅
private:
	string m_bedroom;//卧室
};
class Goodfriend
{
public:
	//好朋友构造函数创建一个Home
	Goodfriend()
	{
		home = new Home;
	}
	//好基友参观函数
	void visit()
	{
		cout << "好朋友正在参观你的" << home->m_livingroom << endl;
		cout << "好朋友正在参观你的" << home->m_bedroom << endl;
	}
private:
	Home* home;
};
void test01()
{
	Goodfriend nn;
	nn.visit();
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

## 成员函数做友元

将类的成员函数，在另一个类中通过friend关键字，可以添加为另一个类的友元

```cpp
这里没有实例代码，因为我在初次学习的时候，实现失败了，，，，难受
    先用前面两种方法吧
```
