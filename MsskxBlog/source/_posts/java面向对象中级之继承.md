---
title: Java面向对象中级(继承)
date: 2021-07-11 09:06:00
updated:
tags: java
categories: java
description: Java面向对象之继承，以及super关键字
---

##  继承：extends（延展拓展）

类图中继承关系画实线，子类指向父类

### 好处：

#### 减少代码冗余，提高代码复用性

#### 便于功能扩展

#### 为多态性的使用提供前提

###  继承性格式:

#### class A extends B { }

#### A ：子类、派生类
#### B ：父类、超类、基类
#### 体现：一旦子类A继承父类B后子类A就获取了父类B中的所有结构
#### 特别的：父类中私有的属性和方法子类继承后任然认为获取了父类中的私有结构，只是因为封装性影响使得子类不能直接调用父类的结构。

#### 子类继承父类以后还可以定义自己特有的属性和方法，实现功能的拓展

#### 父类与子类不同于集合与子集

### 关于继承性的规定

#### 一个父类可以有多个子类

#### 一个子类只能有一个父类：单继承，C++可以多继承，不同于JAVA

#### 子类父类是相对概念，可有多层继承关系

#### 子类直接继承的父类叫直接父类，间接继承的父类叫间接父类

#### 子类继承父类后获取了直接父类和所有间接父类的结构
### 此外
#### 如果没有显式声明一个类的父类，则继承于java.lang.Object类

#### 所有的java类（除它本身）都直接或间接继承于Object类

 #### object是老祖宗

## 方法的重写

### override

#### 1、在子类继承父类中同名同参数的方法进行覆盖操作

#### 2、重写以后，当创建子类以后，通过子类对象调用子父类中同名同参数的方法时，实际是执行子类重写父类的方法

#### 3、重写的规定：

##### 方法声明：权限修饰符返回值方法名（形参列表）{方法体}

##### 约定俗称：子类中叫重写的方法，父类中的叫被重写的方法

###### 1、子类重写的方法的方法名和形参列表与父类被重写的方法的方法名和形参列表相同

###### 2、子类重写的方法的权限修饰符不小于被重写的父类的方法的权限修饰符

###### 3、特殊情况：子类不能重写父类中被声明为private的方法

###### 4、返回值类型：

###### （1）父类被重写的方法的返回值类型是void则子类重写方法返回值类型也只能是void

###### （2）父类被重写的方法的返回值类型是A则子类重写方法返回值类型可以是A类也可以是A类子类

###### （3）父类被重写的方法的返回值类型是基本数据类型则子类重写方法返回值类型必须是相同基本数据类型

###### 5、子类重写的方法抛出的异常类型不大于父类被重写方法抛出的异常类型（具体看异常处理）

###### 6、子类和父类中同名同参数的方法要么都声明为非static的（考虑重写）要么都声明为static的（不是重写）

#### 面试题、区分方法的重载与重写

### 四种访问权限修饰符

projected： **类内部、同一个包、不同包的子类**

## super关键字

### 1、super理解为：**父类的**

### 2、super可以用来调用：属性、方法、构造器

### 3、super的使用：

#### (1)可以在子类的方法或者构造器中。通过使用“super.属性”或者“super.方法”的方式，显式的调用父类中的属性和方法。但是通常情况下，我们省略super

#### (2)特殊情况：当子类和父类定义了同名的属性时，我们要想在子类中调用父类中声明的属性，则必须使用”super.属性“的方式，表明调用的是父类中声明的属性

#### (3)特殊情况：当子类重写父类的方法以后，在子类中调用父类被重写的方法时，则必须显式的使用”super.方法“的方式，表明被调用的是父类中被重写的方法

### 4、super调用构造器

#### (1)在子类构造器中显式的使用super(形参列表)调用父类中声明的指定的构造器

#### (2)super(形参列表)的使用必须声明在子类构造器的首行

#### (3)我们在类的构造器中，针对于this(形参列表)或super(形参列表)只能二选一不能同时出现

#### (4)在构造器首行，没有显式的声明this(形参列表)或super(形参列表)则默认调用父类中的空参的构造器super()

#### (5)在类的多个构造器中至少有一个类的构造器中使用了super(形参列表)，调用父类的构造器

### 5、子类对象实例化过程

#### 1、结果上看:子类继承父类以后获取了父类中声明的属性和方法，在堆空间中会加载所有父类声明的属性。

#### 2、过程上看：当我们通过子类构造器创建子类对象时，我们一定会直接或间接调用其父类构造器，进而调用父类的父类的构造器。。。直到Object。正因为加载过所有父类的结构，所以才可以看到内存中有父类的结构，子类对象才可以考虑进行调用。

#### 3、明确：虽然创建子类对象是调用了父类的构造器，自始至终就创建过一个对象即为new的子类对象。

