---
title: Object类的使用
date: 2021-07-23 12:06:00
updated:
tags: java
categories: java
description: Object类中toString和equals的使用
---

## Object类的使用

1、Object所有java类的根父类

2、如果类的声明未使用extends关键字 指明其父类，则默认父类为java.lang.Object

3、Object类中的功能（属性、方法）具有通用性

​	属性：无

​	方法：equals、tostring、getClass、hashcode、clone、finalize、wait、notify、notifyAll

4、Object类中只声明了一个空参的构造器

面试题：

final、finally、finalize的区别？

## equals

**面试题：==和equals区别**

*==：运算符*

1、可以使用在基本数据类型和引用数据类型变量中

2、如果比较的是**基本数据类型**的变量，比较两个变量保存的**数据**是否相等（不一定类型相同），如果比较的是**引用数据类型**变量，比较的是两个变量的**地址值**是否相同，即两个引用是否指向同一个对象实体。

### equals方法的使用

1、方法而非运算符

2、只能适用于引用数据类型

3、Object类中equals定义：Object类中定义的equals方法和==是相同的，比较的是两个变量的**地址值**是否相同。

4、像String、Date、File都重写了Object的equals方法，比较的是两个对象的“实体内容”

5、通常情况下，比较自定义类是比较实体内容，要对equals进行重写

### 重写equals

原则：比较两个对象的实体内容是否相同

比较常用，一般自动生成

### 总结

通常开发中用的是重写过的，不要被混淆



# tostring

### Object类中tostring的使用

1、当我们输出一个对象的引用是实际上就是调用当前对象的toString（）。

2、Object中toString的定义。

3、像String、Date、File、包装类都重写了Object类中的toString方法。使得在调用对象的toString方法时返回”实体内容“信息。

4、自定义类也可以重写toString方法，当调用此方法时，返回对象的实体内容。

