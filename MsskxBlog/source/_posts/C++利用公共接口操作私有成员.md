---
title: C++中成员属性设置为私有
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++私有成员调用的笔记
---


**<u>优点</u>**：

将成员属性设置为私有，可以自己控制读写权限

对于写权限我们可以检测数据的有效性

**实例**

```cpp
#include<iostream>
using namespace std;
#include<string>
//封装一个人类
class Person
{
public:
	void Modname(string name)//设置名字
	{
		this->name = name;
	}
	string Getname()//读取名字
	{
		return this->name;
	}
	void Modage(int age)//设置年龄
	{
		this->age = age;
	}
	int Getage()//读取年龄
	{
		if (this->age < 0 || this->age>150)
		{
			cout << "你个撒不啦" << endl;
			this->age = 0;
			return this->age;
		}
		return this->age;
	}
	void Modlover(string lover)//设置情人
	{
		this->lover = lover;
	}
	string Getlover()//读取情人
	{
		return this->lover;
	}
private:
	string name;//姓名
	int age;//年龄
	string lover;//情人
};
int main()
{
	Person p;
	//利用公共的接口对私有的成员进行操作
	p.Modage(178);
	p.Modname("二狗");
	p.Modlover("刘玥");
	cout << p.Getname()<<endl;
	cout<<"年龄是："<<p.Getage()<<endl;
	cout << "它的情人是" << p.Getlover()<< endl;
	system("pause");
	return 0;
}
```

注：虽然封装在类里的东西都是私有的，但是可以通过public添加一个公共的接口，对类内私有的成员进行访问