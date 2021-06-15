---
title: Java面向对象初级（属性和方法）
date: 2021-06-12 09:06:00
updated:
tags: java
categories: java
description: Java面向对象之属性和方法
---
# 面向对象初级

## 三条主线：

**1、Java类以及类的成员**：

属性，方法，构造器，代码块，内部类

**2、面向对象的三大特征**：

封装性，继承性，多态性，（抽象性）

**3、其他关键字**：

this，final，static，super，package，abstract......

<u>*"大处着眼，小处着手"*</u>

## 面向过程与面向对象

**面向过程：**强调功能和行为，以函数为最小单位，考虑怎么做

**面向对象：**将功能封装进对象，强调具备功能的对象，以类和对象为最小单位考虑谁来做

**执行者——》指挥者**

## 类和对象

**类是抽象的，概念上的定义**

**对象是实际存在的，也称为实例**

**重点：类的设计**

**设计类：设计类的成员**

### 属性和方法

**属性=成员变量=field=域=字段**

**方法=成员方法=method=函数**

### **落地实现：**

<u>1、创建类、设计类的成员</u>

<u>2、创建类的成员</u>

<u>3、通过“对象.成员”调用对象结构</u>

```java
class Person{
    String name;
    int age=1;
    boolean isMale;
    public void eat(){
        System.out.println("吃饭");
	}
}
//创建对象=类的实例化
Person p1=new Person();
//调用属性和结构
p1.name="mashuai";
p1.eat();
////-------------------------------------
Person p1=new Person();
```

如果创建一个类的多个对象则每个对象的实例都有一套独立的属性(非static)

修改一个对象属性，则不会影响另外一个对象属性

```java
Person p3=p1;
赋的是地址值
```

### 内存解析

<u>堆：存放对象实例</u>

<u>栈：存储局部变量</u>

<u>方法区：类信息，常量，静态变量</u>

###  属性与局部变量

类中属性的使用

属性（成员变量）vs局部变量

**1、相同点**

定义格式相同

都有对应作用域

**2、不同点**

​	2.1、在类中声明的位置不同

​	属性：定义在大括号内

​	局部变量：声明在方法、方法形参、代码块、构造器形参、构造器内的变量

​	2.2、权限修饰符不同

​	属性：可以在声明属性时，指明其权限，使用权限修饰符

​	局部变量：不可以使用权限修饰符

​	2.3、默认初始化值

​	属性：根据其类型都有默认初始化值

​	局部变量：没有默认初始化值，一定要显式赋值

​	特别的形参在调用时赋值即可

​	2.4、在内存中加载的位置不同

​	属性：加载到堆空间

​	局部变量：加载到栈空间

### 方法

描述类应该具有的功能

举例：

权限修饰符 返回值类型 方法名（形参列表）{方法体};

```java
class Customer{
	String name;
    int age;
	public void eat1(){
        System.out.println("吃饭");
	}
    public void eat2(String food){
		System.out.println("吃饭吃"+food);
	}
}
```

## 对象数组练习题

```java
package circle;
/*
*4. 对象数组题目：
定义类Student，包含三个属性：学号number(int)，年级state(int)，成绩
score(int)。
1) 生成随机数：Math.random()，返回值类型double;
2) 四舍五入取整：Math.round(double d)，返回值类型long。
* 创建20个学生对象，学号为1到20，年级和成绩都由随机数确定。
问题一：打印出3年级(state值为3）的学生信息。
问题二：使用冒泡排序按学生成绩排序，并遍历所有学生信息
* */
class Student {
    int number;
    int state;
    int score;
}
public class Test {

    public static void main(String[] args) {
       Student[] Stu=new Student[20];
       for(int i=0;i<Stu.length;i++){
           Stu[i]=new Student();
       }
       //赋学号
        for(int i=0;i<Stu.length;i++){
            Stu[i].number=i+1;
        }
        //赋年级
        for(int i=0;i<Stu.length;i++){
            Stu[i].state=(int)(Math.random()*6)+1;
        }
        //赋成绩
        for(int i=0;i<Stu.length;i++){
            Stu[i].score=(int)(Math.random()*40)+60;
        }
        //打印年级为3
        for(int i=0;i<Stu.length;i++){
            if(3==Stu[i].state){
                System.out.print(Stu[i].score+" ");
            }
        }
        System.out.println("未排序前：");
        //遍历输出
        for(int i=1;i<Stu.length;i++){
            System.out.print(Stu[i].score+" ");
        }
        System.out.println("");
        //冒泡排成绩并输出
        //排序直接排序的是人，不能只改属性
        for(int i=0;i<Stu.length-1;i++){
            for(int j=0;j<Stu.length-i-1;j++){
                Student temp=new Student();
                if(Stu[j+1].score>Stu[j].score){
                    temp=Stu[j+1];
                    Stu[j+1] =Stu[j] ;
                    Stu[j] =temp;
                }
            }
        }
        System.out.println("排序后");
        //遍历输出
        /**
         *
         */
        for(int i=1;i<Stu.length;i++){
            System.out.print(Stu[i].score+" ");
        }
    }
}


```



