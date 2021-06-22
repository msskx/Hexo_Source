---
title: Java面向对象初级（属性和方法）
date: 2021-06-12 09:06:00
updated: 2021-06-20 12:42:00
tags: java
categories: java
description: Java面向对象初级，属性、方法、构造器、this、封装
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



## 匿名对象的使用

```java
class Phone{
    double price;
    public void send(){
        System.out.print();
    }
    public void play(){
        System.out.print();
	}
}
//匿名对象
new Phone().send();
new Phone().play();
Phone phone=new Phone();
//两次调用的不是同一个对象
1、理解：创建的对象没有显式的变量名
2、特征：匿名对象只能调用一次
3、开发中一般：phone.play(new Phone()); 
```

## 自定义数组工具类

## 方法重载

**概念：在同一类中允许存在一个以上的同名方法，只要参数的个数或者类型不同就行**

**判断：**两同一不同：同一个类，相同方法名，（参数列表不同，参数类型不同）

跟修饰符，返回值类型，形参变量名，方法体都无关

**确定调用方法：**确定方法名，参数列表

## 可变个数形参的方法

jdk5.0新增

具体使用：

可变个数形参可构成重载



格式如下

```java
public void show(String ... strs){
    
}
//可利用数组形式调用
```

```java
调用：
    调用方法时传入的参数个数可以是0个，1个，多个
show("hello","world","多个");
show();
```

```java
//不可与此共存，版本问题
public void show(String [] strs){
    
}
//此版本使用方法
show(new String[]{"hello","world"});
```

可变个数形参必须声明在末尾,且最多只能声明一个可变个数形参

```java
public void show(int i,String ... strs){
    
}
```

## 方法参数的值传递机制

基本数据类型，赋值的是变量所保存的数据值

引用数据类型，赋值的是变量所保存的地址值

**方法形参的传递机制：**

1、实参：实际调用时实际传递给形参赋的值

2、描述：

如果参数是基本数据类型，此时实参赋给形参的是实参真实存储的数据值

如果参数是引用数据类型，此时实参赋给形参的是实参真实存储的地址值

### 网红题目

```
int []arr1=new int []{1,2,3};
char[]arr2=new char[]{'1','2','3'};
 System.out.println(arr1);
 System.out.println(arr2);
```

输出结果：

**[I@7c30a502**
**123**

## 递归方法（了解）

一个方法体调用自身

一定要向已知的方向递归

**精髓在于解决问题的范围在变小，否则会栈溢出**

实例：前n项的和，求前n-1项和第n项的和

```java
 public int Sum(int n){
        if(1==n){
            return 1;
        }else{
            return n+Sum(n-1);
        }
    }
```

汉诺塔Java实现：

```java
public class Hanoi {
    /**
     *
     * @param n 盘子的数目
     * @param origin 源座
     * @param assist 辅助座
     * @param destination 目的座
     */
    public void hanoi(int n, char origin, char assist, char destination) {
        if (n == 1) {
            move(origin, destination);
        } else {
            hanoi(n - 1, origin, destination, assist);
            move(origin, destination);
            hanoi(n - 1, assist, origin, destination);
        }
    }

    // Print the route of the movement
    private void move(char origin, char destination) {
        System.out.println("Direction:" + origin + "--->" + destination);
    }

    public static void main(String[] args) {
        Hanoi hanoi = new Hanoi();
        hanoi.hanoi(3, 'A', 'B', 'C');
    }
}
```

## 封装与隐藏

**高内聚**：内部细节不允许外部干涉

**低耦合**：暴露少量方法用于使用

### 封装性体现

1、属性要受数据类型数据 范围制约，在实际问题中要给属性加额外的限制条件

这个条件不能在属性声明时体现，要通过方法去添加

同时避免用户直接对属性赋值，此时针对属性体现封装性

2、<u>封装性体现</u>：将属性私有化，提供公共的方法获取（get）和设置（set）属性

拓展：封装性体现：不对外暴露的私有的方法、单例模式

<u>提高程序可扩展性，可维护性</u>

封装性体现不等同于封装性

### 四种权限修饰符

封装性的体现，需要权限修饰符来配合

1、java规定四种权限（从小到大）

*private、缺省（default）、protected、public*

private：类内部

缺省：类内部、同一个包

protected：类内部、同一个包、不同的子类

public：类内部、同一个包、不同的子类、同一个工程

2、4种权限可用来修饰类以及类的内部结构：属性、方法、内部类、构造器

3、具体的：4种权限可用来修饰类以及类的内部结构：属性、方法、内部类、构造器。

*<u>修饰类的话，只能用：缺省、public</u>*

### 总结封装性

java提供四种权限修饰，来修饰类以及类的内部结构，体现类以及类的内部结构在被调用时的可见性的大小

## 构造器（或构造方法）

***constructor***：建设

***<u>不是方法！！！！！！</u>***

### 一、构造器作用

**创建对象**：new+构造器

**初始化对象信息**

### 二、说明

1、如果没有显式定义构造器，系统默认提供一个空参构造器

2、权限+类名{	}

3、一个类中定义的多个构造器彼此构成重载

4、一旦定义显式构造器，系统不再提供默认的空参构造器

5、一个类中至少要有一个构造器

6、默认构造器权限与类的权限相同

### 三、总结

**属性赋值的先后顺序：**

1、默认初始化

2、显式初始化

3、构造器初始化

4、通过对象赋值

## JavaBean

》》类是公共的

》》有一个无参的公共构造器

》》有属性，而且有set 和 get方法

## UML类图

## this关键字的使用

1、this可以修饰、调用：属性、方法、构造器

2、this修饰属性和方法：this理解为关键对象

可以通过this调用当前的属性和方法，一般可以省略，特殊情况，形参和属性重名时必须使用this表明变量是属性而非形参

3、this修饰调用构造器：

```java 
this();
```

在类的构造器中可以使用this(形参列表)调用本类中指定的**其他**构造器

如果类中有n个构造器，最多n-1个构造器使用this(形参列表)

this(形参列表)必须放在当前构造器首行

构造器内部最多只能一个this(形参列表)

## package和import的使用

### 一、package关键字的使用

1、为了更好地实现项目中类的管理，提出包的概念

2、使用package声明类或接口所属的包，声明在源文件的首行

3、包属于标识符，遵循命名规范，见名知意

4、每”.“一次代表一层文件目录

**补充：同一个包下，不可以命名同名的接口或者类**

### 二、import关键字的使用

import：导入

1、在源文件中显式使用import结构导入指定包下的类、接口

2、声明在package的声明和类的声明之间

3、如果要导入多个结构就并列写出几个

4、可以使用"xxx.*"的方式表示可以导入xxx包下的所有结构

5、如果使用的类或接口是java.lang包下定义的，则可以省略

6、如果使用的类或接口是本包下的，也可以省略

7、如果在源文件中使用了不同包下的同名类则必须有一个类需要以全类名的方式显示

```java
包名.类名
```

8、如果使用xxx.*表明可以调用xxx包下的所有结构，如果使用的是子包下的结构，则仍需要显式导入

9、import static导入指定类或接口中的静态结构：属性、方法

### 三、MVC设计模式

三个层次：视图模型层、控制器层、数据模型层
