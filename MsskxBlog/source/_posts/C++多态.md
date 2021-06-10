---
title: 多态的基本概念
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++多态的基本概念简单理解
---

# 多态的基本概念

多态是C++面向对象的三大特性之一

多态分为两类

**静态多态：**<u>函数重载和运算符重载属于静态多态，复用函数名</u>

**动态多态：**<u>派生类和虚函数实现运行时多态</u>

静态多态和动态多态的**区别：**

静态多态的函数地址**早绑定**-**编译阶段确定函数地址**

动态多态的函数地址**晚绑定**-**运行阶段确定函数地址**

**动态多态满足条件**

1、有继承关系

2、子类重写父类的虚函数

动态多态使用

父类的指针或引用 执行子类对象

**多态好处**

1、组织结构性强

2、可读性强

3、对于前期和后期拓展以及维护性高

# 纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容

因此可以将虚函数改为纯虚函数

语法

```cpp
virtual 返回值类型 函数名 （参数列表）=0;
```

当类中有纯虚函数，这个类也称为抽象类

抽象类特点：

**无法实例化对象**

子类必须重写抽象类中的纯虚函数，否则也属于抽象类

```cpp
#include<iostream>
using namespace std;
#include<string>
class animal
{
public:
	virtual void speak() = 0;
    //只要有一个纯虚函数，这个类称为抽象类
    //抽象类特点：
    //1、无法实例化对象
    //2、抽象类的子类 必须要重写父类中的纯虚函数，否则也属于抽象类，且无法实例化对象
};
class lion: public animal
{
public:	
	void speak()
	{
		cout << "狮子吼叫" << endl;
	}
};
void test01()
{
	lion L;
	L.speak();
	animal* an = new lion;
	an->speak();	
	delete an;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```

做菜案例：

```cpp
#include<iostream>
using namespace std;
#include<string>
class abstructCooking
{
public:
	//买菜
	virtual void Buy() = 0;
	//洗菜
	virtual void Wash() = 0;
	//切菜
	virtual void Cut() = 0;
	//起锅烧油
	virtual void Hotpot() = 0;
	//炒菜
	virtual void Make() = 0;
	//出锅
	virtual void Puttable() = 0;
};
class Fish: public abstructCooking
{
public:	
	//买菜
	virtual void Buy()
	{
		cout << "在菜市场买一条大花鲢鱼" << endl;
	}
	//洗菜
	virtual void Wash()
	{
		cout << "买来的花鲢咱们给它清洗干净" << endl;
	}
	//切菜
	virtual void Cut()
	{
		cout << "咱们给它改一下刀" << endl;
	}
	//起锅烧油
	virtual void Hotpot()
	{
		cout << "起锅烧油，放入葱姜蒜花椒八角桂皮香叶小茴香干辣椒" << endl;
	}
	//炒菜
	virtual void Make()
	{
		cout << "加入郫县豆瓣酱，炒出红油，下入花鲢，一罐啤酒开大火炖" << endl;
	}
	//出锅
	virtual void Puttable()
	{
		cout << "摆盘出锅" << endl;
	}
	
};
class Meat : public abstructCooking
{
public:
	//买菜
	virtual void Buy()
	{
		cout << "在菜市场买一条新鲜猪五花" << endl;
	}
	//洗菜
	virtual void Wash()
	{
		cout << "买来的五花肉咱们给它清洗干净" << endl;
	}
	//切菜
	virtual void Cut()
	{
		cout << "咱们给它改一下刀" << endl;
	}
	//起锅烧油
	virtual void Hotpot()
	{
		cout << "起锅烧油，放入葱姜蒜花椒八角桂皮香叶小茴香干辣椒" << endl;
	}
	//炒菜
	virtual void Make()
	{
		cout << "加入郫县豆瓣酱，炒出红油，下入猪肉，一罐啤酒开大火炖" << endl;
	}
	//出锅
	virtual void Puttable()
	{
		cout << "摆盘出锅" << endl;
	}

};

void dowork(abstructCooking* cook)
{
	cook->Buy();
	cook->Wash();
	cook->Cut();
	cook->Hotpot();
	cook->Make();
	cook->Puttable();
	
	delete cook;
}
void test01()//调用做菜函数
{
	dowork(new Fish);
	cout << "-------------------------------------" << endl;
	dowork(new Meat);
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```

# 虚析构和纯虚析构

多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放是无法调用到子类的析构代码

解决方式：将父类中的析构函数改为虚析构或者纯虚析构

虚析构和纯虚析构共性：

可以解决父类指针释放子类对象

都需要有具体的函数实现

虚析构和纯虚析构区别：
如果是纯虚析构，该类属于抽象类，无法实例化对象

**通过虚析构实现**

```cpp
#include<iostream>
using namespace std;
#include<string>

class Animal
{
public:
	Animal()										
	{
		cout << "Animal的构造函数" << endl;
	}
	virtual ~Animal()
	{
		cout << "Animal的析构函数" << endl;
	}
	//动物叫
	virtual void speak() = 0;
	
};
class Lion: public Animal
{
public:	
	Lion(string name)
	{
		cout << "Lion的构造函数" << endl;
		this->name = name;
	}
	 ~Lion()
	{
		cout << "Lion的析构函数" << endl;
	}
	virtual void speak()
	{
		cout <<name<< "狮子咆哮" << endl;
	}
	string name;
};

void test01()
{
	Animal* an = new Lion("辛巴");
	an->speak();
	delete an;
	
}
int main()
{
	system("color B1");
	test01();
	system("pause");
	
	return 0;
}
 
```

**通过纯虚析构实现**

```cpp
#include<iostream>
using namespace std;
#include<string>
#include<windows.h>
class Animal
{
public:
	Animal()										
	{
		cout << "Animal的构造函数" << endl;
	}
	virtual ~Animal() = 0;
	
	//动物叫
	virtual void speak() = 0;
	
};
Animal::~Animal()
{
	cout << "Animal的析构函数" << endl;
}
//和包含普通纯虚函数的类一样，包含了纯虚析构函数的类也是一个抽象类。不能够被实例化。
class Lion: public Animal
{
public:	
	Lion(string name)
	{
		cout << "Lion的构造函数" << endl;
		this->name = name;
	}
	 ~Lion()
	{
		cout << "Lion的析构函数" << endl;
	}
	virtual void speak()
	{
		cout <<name<< "狮子咆哮" << endl;
	}
	string name;
};

void test01()
{
	Animal* an = new Lion("辛巴");
	an->speak();
	delete an;
	
}
int main()
{
	system("color B1");
	test01();
	/*SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_GREEN);
	printf("Hello");
	SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_RED);
	printf(" World!");*/
	system("pause");
	
	return 0;
}
 
```
