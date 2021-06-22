---
title: C++作业代码块测试
date: 2021-06-16 10:06:00
updated: 
tags: C++
categories: C++
description: C++的代码块
---

## mian

```cpp
#include<iostream>
#include"StudentManage.h"
#include"Grade.h"
#include"Student.h"
using namespace std;

int main()
{
	system("color B1");
	StudentManager stu;
	int chioce;
	while (true)
	{
		//显示菜单
		stu.Show_Menu();
		cout << "请输入您的选择：";
		cin >> chioce;
		switch (chioce)
		{
		case 0:stu.Exit_System();//退出系统
			break;
		case 1:stu.Add_Student();//录入学生
			break;
		case 2:stu.ShowStudent();//显示学籍
			break;
		case 3:stu.DeleteStudent();//删除学生
			break;
		case 4:stu.ModStudent();//修改学生
			break;
		case 5:stu.FindStudent();//查找学生
			break;
		case 6:stu.SortStudent();//学生排序
			break;
		case 7:stu.ClassifyStudent();//分类显示
			break;
		case 8:stu.CleanStudent();//清空系统
			break;
		default://
			system("cls");
			break;
		}
		system("pause");
	}
	return 0;
}
```
## student.h

```cpp
#pragma once
#include<iostream>
using namespace std;
#include<string>
class Student;
typedef class Student
{
public:
	virtual void Show_Info() = 0;//显示个人信息
	virtual string Get_Grade() = 0;//获取年级名称
	int m_id;//学号
	string m_name;//姓名
	string m_sex;//性别
	int  m_grade;//所在年级编号
	string m_class;//班级
	int m_age;//年龄

}STU, * PSTU;
```

## Grade.h

```cpp
#pragma once
#include"Student.h"
typedef class Grade01 :public Student//大一学生类，继承学生类
{
public:
	void Show_Info();//显示个人信息
	string Get_Grade();//获取年级名称
	Grade01(int id, string name, int grade, string sex, string m_class, int m_age);//构造函数
}Grade01, * PGrade01;
typedef class Grade02 :public Student//大二学生类，继承学生类
{
public:
	void Show_Info();//显示个人信息
	string Get_Grade();//获取年级名称
	Grade02(int id, string name, int grade, string sex, string m_class, int m_age);//构造函数
}Grade02, * PGrade02;
typedef class Grade03 :public Student//大三学生类，继承学生类
{
public:
	void Show_Info();//显示个人信息
	string Get_Grade();//获取年级名称
	Grade03(int id, string name, int grade, string sex, string m_class, int m_age);//构造函数
}Grade03, * PGrade03;
typedef class Grade04 :public Student//大一学生类，继承学生类
{
public:
	void Show_Info();//显示个人信息
	string Get_Grade();//获取年级名称
	Grade04(int id, string name, int grade, string sex, string m_class, int m_age);//构造函数
}Grade04, * PGrade04;
```

## Grade.cpp

```cpp
#include"Grade.h"//包含年级学生的头文件
//大一年级学生的实现
Grade01::Grade01(int id, string name, int grade, string sex, string m_class, int m_age)
{
	this->m_id = id;//学号
	this->m_name = name;//姓名
	this->m_grade = grade;//年级
	this->m_class = m_class;//班级
	this->m_sex = sex;//性别
	this->m_age = m_age;//年龄

}//实现大一年级类的构造函数,利用拷贝构造函数赋值
void Grade01::Show_Info()//显示个人信息
{
	cout << "学号：" << this->m_id << " "
		<< "姓名：" << this->m_name << " "
		<< "年级：" << this->Get_Grade() << " "
		<< "性别：" << this->m_sex << " "
		<< "班级：" << this->m_class << " "
		<< "年龄：" << this->m_age << endl;
}
string  Grade01::Get_Grade()//获取年级名称
{
	return (string)"大一";
}
//注：其余三个年级代码，与此类似不再赘述
```
## studentManage.h

```cpp
#pragma once
#include<iostream>
using namespace std;
#include<string>
#include<fstream>//操作文件
#include"Student.h"
#define FILENAME "empFile.txt"//给文件名宏定义，便于后期维护
class StudentManager
{
public:
	//记录人数
	int Student_Num;
	//学生数组的指针
	PSTU* Student_Array;//指针数组用来存Student* 的数组(Student*)* Student_Array;
	//构造函数
	StudentManager();
	//显示菜单
	void Show_Menu();
	//添加学生
	void Add_Student();
	//退出程序
	void Save();
	//保存文件
	void Exit_System();
	//文件是否为空的标志
	bool FileIsEmpty;
	//统计人数
	int get_StudentNum();
	//初始化
	void InitStudent();
	//显示学生
	void ShowStudent();
	//删除学生
	void DeleteStudent();
	//判断职工是否存在,若存在返回位置，若不存在返回-1
	int IsExist(int id);
	//查找学生
	void FindStudent();
	//修改学生
	void ModStudent();
	//按学号排序
	void SortStudent();
	//清空数据
	void CleanStudent();
	//按年级分类显示
	void ClassifyStudent();
	//析构函数
	~StudentManager();
};
```

## StudentManage.cpp
```cpp
//头文件
#include"StudentManage.h"
#include"Grade.h"
```
```cpp
//构造函数
StudentManager::StudentManager()//
{
	ifstream ifs;//创建流对象
	ifs.open(FILENAME, ios::in);//为读文件打开文件
	//文件不存在情况
	if (!ifs.is_open())
	{
		//cout << "文件不存在" << endl;
		this->Student_Num = 0;//初始化人数为零
		this->FileIsEmpty = true;//标志文件为空
		this->Student_Array = NULL;//指针数组为空
		ifs.close();//关闭文件
		return;//函数结束标志
	}
	//文件存在，但是没有记录
	char ch;
	ifs >> ch;
	if (ifs.eof())
	{
		//cout << "文件为空" << endl;
		this->Student_Num = 0;
		this->FileIsEmpty = true;
		this->Student_Array = NULL;//指针数组为空
		ifs.close();//关闭文件
		return;//函数结束标志
	}
	int num = this->get_StudentNum();
	//cout << "学生个数为：" << num << endl;
	this->Student_Num = num;
	//根据学生数创建数组
	this->Student_Array = new PSTU[this->Student_Num];
	this->InitStudent();
}//构造函数
```
```cpp
//显示菜单
void StudentManager::Show_Menu()
{
	cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
	cout << "~~~~~~~~~~~~~~~~学生学籍管理系统~~~~~~~~~~~~~~~~" << endl;
	cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
	cout << "******************（0）退出系统*****************" << endl;
	cout << "******************（1）录入学生*****************" << endl;
	cout << "******************（2）显示学籍*****************" << endl;
	cout << "******************（3）删除学生*****************" << endl;
	cout << "******************（4）修改学生*****************" << endl;
	cout << "******************（5）查找学生*****************" << endl;
	cout << "******************（6）学生排序*****************" << endl;
	cout << "******************（7）分类显示*****************" << endl;
	cout << "******************（8）清空系统*****************" << endl;
	cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
	cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
}
```
```cpp
//退出
void StudentManager::Exit_System()
{
	cout << "欢迎下次使用" << endl;
	system("pause");
	exit(0);
}
```
```cpp
//添加
void StudentManager::Add_Student()
{
	cout << "请输入添加学生数量" << endl;
	int addnum;
	cin >> addnum;
	if (addnum > 0)
	{
		//计算新空间大小
		int newsize = this->Student_Num + addnum;
		//开辟空间
		PSTU* newspace = new PSTU[newsize];
		//将源空间的内容存放到新空间下
		if (this->Student_Array != NULL)
		{
			for (int i = 0; i < this->Student_Num; i++)
			{
				newspace[i] = this->Student_Array[i];
			}
		}
		//输入新数据
		for (int i = 0; i < addnum; i++)
		{
			int id;
			string name;
			int select;
			string sex;
			string m_class;
			int m_age;
			cout << "请输入第" << i + 1 << "个学生学号" << endl;
			cin >> id;
			cout << "请输入第" << i + 1 << "个学生姓名" << endl;
			cin >> name;
			cout << "请输入第" << i + 1 << "个学生年级编号" << endl;
			cout << "1、大一" << endl;
			cout << "2、大二" << endl;
			cout << "3、大三" << endl;
			cout << "4、大四" << endl;
			cin >> select;
			cout << "请输入第" << i + 1 << "个学生性别" << endl;
			cin >> sex;
			cout << "请输入第" << i + 1 << "个学生班级" << endl;
			cin >> m_class;
			cout << "请输入第" << i + 1 << "个学生年龄" << endl;
			cin >> m_age;
			PSTU student = NULL;
			switch (select)
			{
			case 1://大一
				student = new Grade01(id, name, 1, sex, m_class, m_age);
				break;
			case 2://大2
				student = new Grade02(id, name, 2, sex, m_class, m_age);
				break;
			case 3://大3
				student = new Grade03(id, name, 3, sex, m_class, m_age);
				break;
			case 4://大4
				student = new Grade04(id, name, 4, sex, m_class, m_age);
				break;
			default:
				break;
			}

			newspace[this->Student_Num + i] = student;
		}
		//释放原有空间
		delete[]this->Student_Array;
		//更新空间指向
		this->Student_Array = newspace;
		//更新学生个数
		this->Student_Num = newsize;
		//更改为空标志
		this->FileIsEmpty = false;
		//提示
		cout << "添加成功" << addnum << "个学生" << endl;
		this->Save();//保存文件
	}
	else {
		cout << "输入有误" << endl;
	}
	system("pause");
	system("cls");
}
```
```cpp
//保存文件
void StudentManager::Save()
{
	ofstream ofs;
	ofs.open(FILENAME, ios::out);//以写文件的方式打开文件
	for (int i = 0; i < this->Student_Num; i++)
	{
		ofs << this->Student_Array[i]->m_id << " "
			<< this->Student_Array[i]->m_name << " "
			<< this->Student_Array[i]->m_grade << " "
			<< this->Student_Array[i]->m_sex << " "
			<< this->Student_Array[i]->m_class << " "
			<< this->Student_Array[i]->m_age << " " << endl;
	}
	ofs.close();
}
```
```cpp
//获取学生个数
int StudentManager::get_StudentNum()
{
	ifstream ifs;
	ifs.open(FILENAME, ios::in);
	int id;
	string name;
	int grade;
	string sex;
	string m_class;
	int m_age;
	int num = 0;
	while (ifs >> id && ifs >> name && ifs >> grade && ifs >> sex && ifs >> m_class && ifs >> m_age)
	{
		//记录人数
		num++;
	}
	ifs.close();
	return num;
}
```
```cpp
//初始化
void StudentManager::InitStudent()
{
	ifstream ifs;
	ifs.open(FILENAME, ios::in);
	int id;
	string name;
	int grade;
	int index = 0;
	string sex;
	string m_class;
	int m_age;
	while (ifs >> id && ifs >> name && ifs >> grade && ifs >> sex && ifs >> m_class && ifs >> m_age)
	{
		PSTU student = NULL;//根据年级创建PSTU的对象
		if (id == 1)
		{
			student = new Grade01(id, name, grade, sex, m_class, m_age);
		}
		else if (id == 2)
		{
			student = new Grade02(id, name, grade, sex, m_class, m_age);
		}
		else if (id == 3)
		{
			student = new Grade03(id, name, grade, sex, m_class, m_age);
		}
		else
		{
			student = new Grade04(id, name, grade, sex, m_class, m_age);
		}
		//存放在数组中
		this->Student_Array[index] = student;
		index++;

	}
}
```
```cpp
//显示
void StudentManager::ShowStudent()
{
	if (this->FileIsEmpty)
	{
		cout << "文件为空或者不存在" << endl;
	}
	else
	{
		for (int i = 0; i < this->Student_Num; i++)
		{
			//利用多态调用接口
			this->Student_Array[i]->Show_Info();
		}
	}
	system("pause");
	system("cls");
}
```
```cpp
//删除
void StudentManager::DeleteStudent()
{
	if (this->FileIsEmpty)
	{
		cout << "文件不存在或者记录为空" << endl;
	}
	else
	{
		cout << "请输入要删除的学生学号" << endl;
		int id = 0;
		cin >> id;
		int index = this->IsExist(id);
		if (index != -1)
		{
			for (int i = index; i < this->Student_Num - 1; i++)
			{
				this->Student_Array[i] = this->Student_Array[i + 1];
			}
			this->Student_Num--;
			this->Save();//删除后同步数据到文件
			cout << "删除成功" << endl;
		}
		else
		{
			cout << "删除失败，未找到该学生" << endl;
		}
	}
	system("pause");
	system("cls");
}
```
```cpp
//查找
void StudentManager::FindStudent()
{
	if (this->FileIsEmpty)
	{
		cout << "文件不存在或者记录为空！" << endl;
	}
	else
	{
		cout << "请输入查找的方式：" << endl;
		cout << "1、按编号查找" << endl;
		cout << "2、按姓名查找" << endl;

		int select = 0;
		cin >> select;
		if (select == 1)//按照学号查找
		{
			int id;
			cout << "请输入查找的学号" << endl;
			cin >> id;
			int ret = this->IsExist(id);
			if (ret != -1)
			{
				cout << "查找成功，该学生信息如下" << endl;
				this->Student_Array[ret]->Show_Info();
			}
			else
			{
				cout << "查找失败，查无此人" << endl;
			}
		}
		else if (select == 2)//按姓名查找
		{
			string name;
			cout << "请输入查找的姓名" << endl;
			cin >> name;
			bool flag = false;//查找到的标志
			for (int i = 0; i < this->Student_Num; i++)
			{
				if (this->Student_Array[i]->m_name == name)
				{
					cout << "查找成功，信息如下" << endl;
					flag = true;
					this->Student_Array[i]->Show_Info();
				}
			}
			if (flag == false)
			{
				cout << "查找失败，查无此人！！" << endl;
			}
		}
		else
		{
			cout << "输入选项有误" << endl;
		}
	}
	system("pause");
	system("cls");
}
```
```cpp
//修改
void StudentManager::ModStudent()
{
	if (this->FileIsEmpty)
	{
		cout << "文件不存在，或记录为空" << endl;
	}
	else
	{
		cout << "请输入要修改的学生学号" << endl;
		int id;
		cin >> id;
		int ret = this->IsExist(id);
		if (ret != -1)
		{
			delete this->Student_Array[ret];
			int newid = 0;
			string newname = "";
			int select = 0;
			string newsex;
			string newclass;
			int newage;
			cout << "查到" << id << "号学生，请输入新学号" << endl;
			cin >> newid;
			cout << "请输入新姓名" << endl;
			cin >> newname;
			cout << "请输入年级" << endl;
			cout << "1、大一" << endl;
			cout << "2、大二" << endl;
			cout << "3、大三" << endl;
			cout << "4、大四" << endl;
			cin >> select;
			cout << "请输入班级" << endl;
			cin >> newclass;
			cout << "请输入年龄" << endl;
			cin >> newage;
			Student* student = NULL;
			switch (select)
			{
			case 1://大一
				student = new Grade01(newid, newname, 1, newsex, newclass, newage);
				break;
			case 2://大2
				student = new Grade02(newid, newname, 2, newsex, newclass, newage);
				break;
			case 3://大3
				student = new Grade03(newid, newname, 3, newsex, newclass, newage);
				break;
			case 4://大4
				student = new Grade04(newid, newname, 4, newsex, newclass, newage);
				break;
			default:
				break;
			}
			//更新数据到数组中
			this->Student_Array[ret] = student;
			cout << "修改成功" << endl;
			//保存文件
			this->Save();

		}
		else
		{
			cout << "修改失败，查无此人" << endl;
		}
		system("pause");
		system("cls");
	}
}
```
```cpp
//判断是否存在
int StudentManager::IsExist(int id)
{
	int index = -1;
	for (int i = 0; i < this->Student_Num; i++)
	{
		if (this->Student_Array[i]->m_id == id)
		{
			index = i;
			break;
		}
	}
	return index;
}
```
```cpp
//排序
void StudentManager::SortStudent()
{
	if (this->FileIsEmpty)
	{
		cout << "文件不存在或者记录为空" << endl;
		system("pause");
		system("cls");

	}
	else
	{
		cout << "请选择排序方式： " << endl;
		cout << "1、按学号进行升序" << endl;
		cout << "2、按学号进行降序" << endl;

		int select = 0;
		cin >> select;

		for (int i = 0; i < this->Student_Num; i++)
		{
			int minOrmax = i;
			for (int j = i + 1; j < this->Student_Num; j++)
			{
				if (select == 1)
				{
					if (this->Student_Array[minOrmax]->m_id > this->Student_Array[j]->m_id)
					{
						minOrmax = j;
					}
				}
				else
				{
					if (this->Student_Array[minOrmax]->m_id < this->Student_Array[j]->m_id)
					{
						minOrmax = j;
					}
				}
			}
			if (i != minOrmax)
			{
				Student* temp = this->Student_Array[i];
				this->Student_Array[i] = this->Student_Array[minOrmax];
				this->Student_Array[minOrmax] = temp;
			}
		}
		cout << "排序成功" << endl;
		this->Save();
		system("pause");
		system("cls");
	}
}
```
```cpp
//清空
void StudentManager::CleanStudent()
{
	cout << "确认清空？" << endl;
	cout << "1、确认" << endl;
	cout << "2、返回" << endl;
	int select = 0;
	cin >> select;
	if (select == 1)
	{
		//打开模式ios::trunc如果存在就删除文件并重新创建
		ofstream ofs(FILENAME, ios::trunc);
		ofs.close();
		if (this->Student_Array != NULL)
		{
			for (int i = 0; i < this->Student_Num; i++)
			{
				if (this->Student_Array[i] != NULL)
				{
					delete this->Student_Array[i];
				}
			}
			this->Student_Num = 0;
			delete[] this->Student_Array;
			this->Student_Array = NULL;
			this->FileIsEmpty = true;
		}
		cout << "清空成功" << endl;
	}
	system("pause");
	system("cls");
}
```
```cpp
//分类显示
void StudentManager::ClassifyStudent()
{
	cout << "大一：" << endl;
	for (int i = 0; i < this->Student_Num; i++)
	{
		if (this->Student_Array[i]->m_grade == 1)
		{
			this->Student_Array[i]->Show_Info();
		}
	}
	cout << endl;
	cout << "大二：" << endl;
	for (int i = 0; i < this->Student_Num; i++)
	{
		if (this->Student_Array[i]->m_grade == 2)
		{
			this->Student_Array[i]->Show_Info();
		}
	}
	cout << endl;
	cout << "大三：" << endl;
	for (int i = 0; i < this->Student_Num; i++)
	{
		if (this->Student_Array[i]->m_grade == 3)
		{
			this->Student_Array[i]->Show_Info();
		}
	}
	cout << endl;
	cout << "大四：" << endl;
	for (int i = 0; i < this->Student_Num; i++)
	{
		if (this->Student_Array[i]->m_grade == 4)
		{
			this->Student_Array[i]->Show_Info();
		}
	}
	system("pause");
	system("cls");
}
```
```cpp
//析构函数
StudentManager::~StudentManager()
{
	if (this->Student_Array != NULL)
	{
		delete[]this->Student_Array;
	}
}
```

