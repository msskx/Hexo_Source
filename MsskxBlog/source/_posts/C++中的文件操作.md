---
title: 文件操作
date: 2021-06-10 22:06:00
updated: 2021-06-11 17:55:07
tags: C++
categories: C++
description: C++文件操作的使用笔记
---



**写在前面**

<u>ofstream写文件，也就是对文件的输出，所以out，以O开头</u>

<u>ofstream的成员函数中包含write写文件</u>

<u>ifstream读文件，也就是文件对外输入，所以in，以I开头</u>

<u>ifstream的成员函数中包含read读文件</u>

**操作文件包含头文件fstream**

## 类型：

文本文件：ASCLL存储

二进制文件：二进制存储

## 操作文件三大类

1、ofstream：写操作

2、ifstream：读操作

3、fstream：读写操作

## 文本文件操作

### 写文件

1、包含头文件

fstream

2、创建流对象

ofstream ofs

3、打开文件

ofs.open（”文件路径“，"打开方式"）;

4、写数据

ofs<<"写入的数据"；

5、关闭文件

ofs.close

| 打开方式    | 解释                       |
| ----------- | -------------------------- |
| ios::in     | 为读文件而打开文件         |
| ios::out    | 为写文件打开文件           |
| ios::ate    | 初始位置：文件尾           |
| ios::app    | 追加方式写文件             |
| ios::trunc  | 如果文件存在先删除，再创建 |
| ios::binary | 二进制文件                 |

 注意：文件打开方式可以配合使用，利用|操作符

例如：用二进制方式写文件

```cpp
ios::binary|ios::out 
```

```cpp
#include<iostream>
#include<fstream>
using namespace std;
void test()
{
	//1、包含头文件
	//2、创建流对象
	ofstream ofs;
	//3、打开文件
	ofs.open("资料.txt",ios::out);
	//4、写数据
	ofs << "此情可待成追忆，只是当时已惘然";
	//5、关闭文件
	ofs.close();
}
int main()
{
	test();
	system("pause");
}
```

总结：

文件操作必须包含头文件fstream

读文件可以利用ofstream，或者fstream类

打开文件时候需要操作文件的路径，以及打开方式

利用<<可以向文件中写数据

操作完毕要关闭文件

### 读文件

1、包含头文件

2、创建流对象

ifstream ifs

3、打开文件判断是否打开

ifs.open（“资料”，iOS::in）;

ifs.is_open返回布尔类型用if语句判断文件是否打开成功

4、读数据(四种方法)

```cpp
1/

char buf[1024]={0};

while(ifs>>buf)

{

cout<<buf<<endl;

}
```

```cpp
2/

char buf[1024]={0};

while(ifs.getline(buf,sizeof(buf)))

{

cout<<buf<<endl;

}
```



```cpp
3/

string buf

while(getline(ifs,buf))

{

cout<<buf<<endl;

}
```



```cpp
4/不推荐

char c;

while((c=ifs.get())!=EOF)//end of file

{

cout<<c;
}
```



5、关闭文件

ifs.close()

```cpp
#include<iostream>
#include<fstream>
#include<string>
using namespace std;
void test()
{
	//1、包含头文件
	//2、创建流对象
	ifstream ifs;
	//3、打开文件
	ifs.open("资料.txt", ios::in);
	if (ifs.is_open() == false)
	{
		cout << "文件打开失败！" << endl;
	}
	//4、读数据
	string buf;
	while (getline(ifs, buf))
	{
		cout << buf << endl;
	}
	//5、关闭文件
	ifs.close();
}
int main()
{
	test();
	system("pause");
}
```

## 二进制文件操作

### 写文件

ios::binary

二进制方式写文件主要利用流对象调用成员函数write

函数原型：ostream&  write(const char*  buffer ,int len)

参数解释：字符指针buffer 指向内存中一段存储空间，len是读写的字节数

```cpp
#include<iostream>
#include<fstream>
#include<string>
using namespace std;
class Person
{
public:
	char name[64];
	int age;
};
void test()
{
	//1、包含头文件
	//2、创建流对象
	ofstream ofs;
	//也可以创建流对象时候直接ifstream ifs("资料.txt",ios::out|ios::binary);
	//3、打开文件
	ofs.open("资料.txt", ios::out | ios::binary);//用二进制的方式打开文件
	//4、写文件
	Person p = { "张三",18 };
	ofs.write ((const char*)&p, sizeof(Person));//根据函数要求，对p进行强转
	//5、关闭文件
	ofs.close();
}
int main()
{
	test();
	system("pause");
}
```



### 读文件

二进制方式读文件主要利用流对象调用成员函数read

函数原型istream& read(char * bufer,int len);

参数解释：字符指针buffer指向内存中的一段存储空间，len是读写的字节数

```cpp
#include<iostream>
#include<fstream>
#include<string>
using namespace std;
class Person
{
public:
	char name[64];
	int age;
};
void test()
{
	//1、包含头文件
	//2、创建流对象
	ifstream ifs;
	//3、打开文件
	ifs.open("资料.txt", ios::in | ios::binary);
	if (ifs.is_open() == false)
	{
		cout << "文件打开失败！" << endl;
		return;
	}
	//4、读文件
	Person p;
	ifs.read((char*)&p, sizeof(Person));
	cout << "姓名：" << p.name << "年龄" << p.age << endl;
	//5、关闭文件
	ifs.close();
}
int main()
{
	test();
	system("pause");
}
```
