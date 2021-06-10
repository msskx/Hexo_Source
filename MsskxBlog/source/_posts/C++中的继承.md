---
title: 继承
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++继承的简单理解
---

# 继承

**继承是C++面向对象三大特性之一**

定义一些类时下级成员除了拥有上一级的共性，还有自己的特性

这时候考虑继承，减少重复代码

## 继承的基本语法

**继承的好处**：减少重复代码

**语法**：class  子类：继承方式  父类

**子类** 也称为派生类

**父类** 也称为基类

```cpp
#include<iostream>
using namespace std;
#include<string>
class BasePage 
{
public:
	void head()
	{
		cout << "____________________________" << endl;
		cout << "这是一个共享的头部页面" << endl;
	}
	void footer()
	{
		cout << "这是一个共享的尾部页面" << endl;
	}
};
//构建JAVA
class JAVA : public BasePage
{
public:
	void java()
	{
		cout << "我是一只快乐的小java" << endl;
	}
};
//构建C++
class CPP : public BasePage
{
public:
	void cpp()
	{
		cout << "我是一只快乐的小C++" << endl;
	}
};
//构建Python
class Python: public BasePage
{
public:
	void python()
	{
		cout << "我是一只快乐的小python" << endl;
	}

};
void test01()
{
	JAVA ja;
	ja.head();
	ja.java();
	ja.footer();
	CPP cp;
	cp.head();
	cp.cpp();
	cp.footer();
	Python py;
	py.head();
	py.python();
	py.footer();

}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

## 继承方式

公共继承

保护继承

私有继承

![吞吞吐吐](C:\Users\lenovo\Desktop\吞吞吐吐.png)

# 继承中的对象模型

从父类继承过来的成员，私有成员只是被隐藏了，还是会继承下去

```CPP
#include<iostream>
using namespace std;
#include<string>
class BasePage 
{
public:
	int a;
	int b;
private:
	int c;
};
//构建JAVA
class JAVA : public BasePage
{
public:
	int f;
};

void test01()
{
	JAVA ja;
	cout << "size of java=" << sizeof(ja) << endl;//运行结果是16
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```

## 父类中所有非静态成员函数属性都会被子类继承下去

# 继承中的构造和析构顺序

子类继承父类后，当子类创建对象，也会调用父类的构造函数

```cpp
#include<iostream>
using namespace std;
#include<string>
class BasePage 
{
public:
	BasePage()
	{
		cout << "父类构造函数" << endl;
	}
	~BasePage()
	{
		cout << "父类构造函数" << endl;
	}
};
class JAVA : public BasePage
{
public:
	JAVA()
	{
		cout << "子类构造函数" << endl;
	}
	~JAVA()
	{
		cout << "子类构造函数" << endl;
	}
};

void test01()
{
	JAVA ja;
	
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```

#### 继承中：先有父亲再有儿子，析构刚好相反，白发人送黑发人

# 继承同名成员处理方式   

**访问子类同名成员：直接访问即可**

**访问父类同名成员：需要加作用域**

```cpp
#include<iostream>
using namespace std;
#include<string>
class BasePage 
{
public:
	
	int m_a;
	void play()
	{
		cout << "父亲玩" << endl;
	}
};
class JAVA : public BasePage
{
public:
	
	int m_a;
	void play()
	{
		cout << "孩子玩" << endl;
	}
};

void test01()
{
	JAVA java;
	java.m_a = 999;
	java.BasePage::m_a = 999;
	cout << "java.m_a=" << java.m_a << endl;
	cout << "java.m_a=" << java.BasePage::m_a << endl;
	java.play();
	java.BasePage::play();
	
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```



**当子类与父类拥有同名成员函数，子类会隐藏父类中所有版本的同名成员函数（包括函数重载）**

**如果想访问父类中被隐藏的同名成员函数，需要加父类的作用域**

# 继承同名静态成员的处理方式

静态成员与非静态成员出现同名处理方式一致

只不过有两种访问方式，一种通过对象，一种通过类

```cpp
#include<iostream>
using namespace std;
#include<string>
class BasePage 
{
public:
	
	static int m_a;
	static void play()
	{
		cout << "父亲玩" << endl;
	}
};
int  BasePage::m_a = 9;
class JAVA : public BasePage
{
public:
	
	static int m_a;
	static void play()
	{
		cout << "孩子玩" << endl;
	}
};
int  JAVA::m_a = 90;
void test01()
{
	JAVA java;
	//通过对象调用
	java.m_a = 999;
	java.BasePage::m_a = 999;
	cout << "java.m_a=" << java.m_a << endl;
	cout << "java.m_a=" << java.BasePage::m_a << endl;
	java.play();
	java.BasePage::play();
	//通过类名调用
	cout << "JAVA::m_a=" << JAVA::m_a << endl;
	cout << "BasePage::m_a=" << BasePage::m_a << endl;
	cout << "JAVA::BasePage::m_a=" << JAVA::BasePage::m_a << endl;
	JAVA::play();
	BasePage::play();
	JAVA::BasePage::play();

	
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```

# 多继承语法

C++中允许一个类继承多个类

语法

class 子类 : 继承方式  父类1，继承方式 父类2……

多继承中可能会引发父类中有同名成员出现，**需要加作用域区分**

**C++实际开发中不建议多继承、**

```cpp
#include<iostream>
using namespace std;
#include<string>
class Base1
{
public:
	int m_A=900;
	
};

class Base2
{
public:
	int m_A=299;

};

class JAVA : public Base1,public Base2
{
public:
	int m_c=4;
	int m_d=3;
	
};

void test01()
{
	JAVA java;
	cout << "sizeof (JAVA)=" << sizeof(java) << endl;
	cout << "JAVA m_c=" << java.m_c << endl;
	cout << "JAVA Base1:: m_A=" << java.Base1::m_A << endl;
	cout << "JAVA Base2:: m_A=" << java.Base2::m_A << endl;
	
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```

# 菱形继承问题

两个派生类继承同一个基类

又有某个类同时继承两个派生类

例如狮子继承了动物数据，老虎也继承了动物数据，当狮虎兽使用数据时就会产生二义性

狮虎兽继承了来自动物的数据两份，我们应该清楚只要一份就行

利用虚继承解决菱形继承问题

```cpp
#include<iostream>
using namespace std;
#include<string>
class animal
{
public:
	int m_A;
};
class lion:virtual public animal
{
public:	
};
class teeger : virtual public animal
{
public:
};
class lioner :public lion, public teeger
{
public:

};
void test01()
{
	lioner l;
	l.lion::m_A = 88;
	l.teeger::m_A = 99;
	cout << "lion m_a=" << l.lion::m_A << endl;
	cout << "teeger m_a=" << l.teeger::m_A << endl;
	cout << "lioner m_a=" << l.m_A << endl;//利用纯虚继承后可以直接通过对象访问
}
int main()
{
	test01();
	system("pause");
	return 0;
}
 
```
