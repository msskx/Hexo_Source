---
title: Java入门基础笔记
date: 2021-06-09 16:45:00
updated: 2021-06-11 11:55:07
tags: java
categories: java
description: 刚学Java时候的基础笔记，包含面向对象之前的一系列基础知识
---

# 基本语法

## 关键字和保留字

**被java赋予了特殊含义，做专门用途的字符串**

## 标识符

## 变量

## 运算符

## 流程控制

鄙人今天开始正式学习java，历经困难终于写下第一个java程序
```java
package com.java_01;

public class HelloWorld {
	public static void main(String[] args){
	System.out.println("你好，尚柯序");
	}

}
```

**补充**
通过DOS命令执行
首先写好一个.java后缀的文件
用记事本写好后再改后缀
**注意文件名一定与类名相同**
利用DOS命令进入.java文件所在的文件夹
利用javac+[ ]+文件名进行编译
编译成功后会出现一个相同名称,class文件
这样就编译成功
然后直接在文件夹内利用DOS命令即可成功执行

**我能希望坚持下去**
**加油**



# **变量**
###  整形int
### 小数double
### 字符型char
**目前字符型char A=''中，只能放一个字符。**
## 这是第一次尝试的代码
```java
package com.java_01;
public class HelloWorld{
	public static void main(String[] args) {
		System.out.println("三种变量的学习");
		System.out.println("1、整形");
		int a;
		a=56;
		System.out.println(a);
		System.out.println("2、小数");
		double b=3.1415925;
		System.out.println(b);
		System.out.println("3、字符串");
		char c='尚';
		char d='柯';
		char e='序';
		System.out.println(c);
		System.out.println(d);
		System.out.println(e);
		}
}
```
### 常量
**常量就是在变量前面加一个final，然后常量不可以改变**
**一般常量用大写字母表示，便于认出，一般不用汉字作为表示符，因为安全隐患太多。**
```java
final int A=10;
System.out.println(A);
```
### 第二次添加
```java
package com.java_01;
public class HelloWorld{
	public static void main(String[] args) {
		int a=10;
		int b=10000;
		float c=1.34f;
		double d=2.3456712;
		char e='a';
		char f='j';
		boolean g=true;
		System.out.println(a);
		System.out.println(b);
		System.out.println(c);
		System.out.println(d);
		System.out.println(e);
		System.out.println(f);
		System.out.println(g);
		
	}
}
```
**注意float后面要加f；**
**bollean**




# 算数运算符
>算数运算符与数学中所表达的含义是一样的
>Java中的算数运算符详细如下：
>表格中的整数变量A的值为10，变量B的值为20：



| 操作符 | 描述                              | 例子                               |
| ------ | --------------------------------- | ---------------------------------- |
| +      | 加法 - 相加运算符两侧的值         | A + B 等于 30                      |
| -      | 减法 - 左操作数减去右操作数       | A – B 等于 -10                     |
| *      | 乘法 - 相乘操作符两侧的值         | A * B等于200                       |
| /      | 除法 - 左操作数除以右操作数       | B / A等于2                         |
| ％     | 取余 - 左操作数除以右操作数的余数 | B%A等于0                           |
| ++     | 自增: 操作数的值增加1             | B++ 或 ++B 等于 21（区别详见下文） |
| --     | 自减: 操作数的值减少1             | B-- 或 --B 等于 19（区别详见下文） |

**实例**
```java
public class Test {

  public static void main(String[] args) {
     int a = 10;
     int b = 20;
     int c = 25;
     int d = 25;
     System.out.println("a + b = " + (a + b) );
     System.out.println("a - b = " + (a - b) );
     System.out.println("a * b = " + (a * b) );
     System.out.println("b / a = " + (b / a) );
     System.out.println("b % a = " + (b % a) );
     System.out.println("c % a = " + (c % a) );
     System.out.println("a++   = " +  (a++) );
     System.out.println("a--   = " +  (a--) );
     // 查看  d++ 与 ++d 的不同
     System.out.println("d++   = " +  (d++) );
     System.out.println("++d   = " +  (++d) );
  }
}
```
**运行结果**
```java
a + b = 30
a - b = -10
a * b = 200
b / a = 2
b % a = 0
c % a = 5
a++   = 10
a--   = 11
d++   = 25
++d   = 27
```
## 自增自减运算符
**1、自增运算（++）自减运算（--）运算符是一种特殊的运算符，在运算符中需要两个操作数来进行运算，而且自增自减运算符是一个操作数。**
```java
public class Test{
    public static void main(String[] args){
        int a = 3;//定义一个变量；
        int b = ++a;//自增运算
        int c = 3;
        int d = --c;//自减运算
        System.out.println("进行自增运算后的值等于"+b);
        System.out.println("进行自减运算后的值等于"+d);
    }
}
```
运行结果为
```java
进行自增运算后的值等于4
进行自减运算后的值等于2
```
**解析**
```java
int b = ++a; 拆分运算过程为: a=a+1=4; b=a=4, 最后结果为b=4,a=4
int d = --c; 拆分运算过程为: c=c-1=2; d=c=2, 最后结果为d=2,c=2
```
**2、前缀自增自减法(++a,--a): 先进行自增或者自减运算，再进行表达式运算。**

**3、后缀自增自减法(a++,a--): 先进行表达式运算，再进行自增或者自减运算 实例：**
```java

public class Test{
    public static void main(String[] args){
        int a = 5;//定义一个变量；
        int b = 5;
        int x = 2*++a;
        int y = 2*b++;
        System.out.println("自增运算符前缀运算后a="+a+",x="+x);
        System.out.println("自增运算符后缀运算后b="+b+",y="+y);
    }
}
```

运行结果为：
```java
自增运算符前缀运算后a=6，x=12
自增运算符后缀运算后b=6，y=10
```
# 关系运算符
>下表为java中的一些关系运算符，其中整形变量A的值为10，变量B的值为20

格中的实例整数变量A的值为10，变量B的值为20：

| 运算符 | 描述                                                         | 例子             |
| ------ | ------------------------------------------------------------ | ---------------- |
| = =    | 检查如果两个操作数的值是否相等，如果相等则条件为真。         | （A == B）为假。 |
| !=     | 检查如果两个操作数的值是否相等，如果值不相等则条件为真。     | (A != B) 为真。  |
| >      | 检查左操作数的值是否大于右操作数的值，如果是那么条件为真。   | （A> B）为假。   |
| <      | 检查左操作数的值是否小于右操作数的值，如果是那么条件为真。   | （A <B）为真。   |
| >=     | 检查左操作数的值是否大于或等于右操作数的值，如果是那么条件为真。 | （A> = B）为假。 |
| <=     | 检查左操作数的值是否小于或等于右操作数的值，如果是那么条件为真。 | （A <= B）为真。 |
**实例**
```java
public class Test {
  public static void main(String[] args) {
     int a = 10;
     int b = 20;
     System.out.println("a == b = " + (a == b) );
     System.out.println("a != b = " + (a != b) );
     System.out.println("a > b = " + (a > b) );
     System.out.println("a < b = " + (a < b) );
     System.out.println("b >= a = " + (b >= a) );
     System.out.println("b <= a = " + (b <= a) );
  }
}
```
**上述实例编译结果如下**
```java
a == b = false
a != b = true
a > b = false
a < b = true
b >= a = true
b <= a = false
```

# java中的随机数
首先查看API中的语法

| static double          | random()                      |
| ---------------------- | ----------------------------- |
| 返回带正号的 double 值 | 该值大于等于 0.0 且小于 1.0。 |

**利用Math类中的random（）生成一个随机数，这个数是一个Double的变量，而且范围是[0.0 , 1.0]**
看个人需求，可以将随机数的类型转换为其他类型，当然在“大转小”的过程中，会有一些精度的损失
### 通过运算可以将生成随机数的范围转换为我们想要的范围
**比如：**我想要一个int类型的，而且范围在[1 , 6]之间的数
```java
//一步一步慢慢来看
Math.random()------>[0.0,1.0)
(int)(Math.random())------>[0, 1)
(Math.random()*6)------>[0,6)
//由于不等于6，也就是5.几 ，转换后会损失精度
(int)(Math.random()*6)------>[0,5]
(int)(Math.random()*6)+1------>[1,6]
```
### 下面是我做的一个例子
```java
public class HelloWorld{
	public static void main(String[] args) {
		System.out.println("随机数抽奖系统");
		//[24,78],54
		int num=(int)(Math.random()*55)+24;
		if(num>51) {
			System.out.println("你会成功");
		}else {
			System.out.println("你一定会成功");
		}
	}
}
```
```java
import java.util.*;
public class HelloWorld{
	public static void main(String[] args) {
		System.out.println("会员购物时可以享受不同的购物折扣");
		System.out.println();
		System.out.println("请输入您的购物积分");
		Scanner input=new Scanner(System.in);
		int num=(int)(Math.random()*4001)+5000;
		System.out.println("您的会员积分是"+num);
		if(num>=8000) {
			System.out.println("大爷，您享受0.6折");
		}else if(num>=4000) {
			System.out.println("老板，您享受0.8折");
		}else if(num>=2000) {
			System.out.println("兄弟，您享受0.9折");
		}else {
			System.out.println("你享受个屁，你配吗？");
		}
	}
}
```





public class TestSwitch{
	public static void main(String[] args){
		/*
		实现一个功能：
		根据给出的学生分数，判断学生的等级：
		>=90  -----A
		>=80  -----B
		>=70  -----C
		>=60  -----D
		<60   -----E
		
```java
		用if分支：
		if(score>=90){
			
		}else if(score>=80){
			
		}
		*/
		//1.给出学生的成绩：
		int score = 167;
		//2.根据成绩判断学生的等级：
		switch(score/10){
			case 10 : 
			case 9 : System.out.println("A级");break;
			case 8 : System.out.println("B级");break;
			case 7 : System.out.println("C级");break;
			case 6 : System.out.println("D级");break;
			default:System.out.println("成绩错误");break;
			case 5 :  
			case 4 :  
			case 3 :  
			case 2 :  
			case 1 :  
			case 0 : System.out.println("E级");break;
			
		}
		/*
		【1】语法结构：
		switch(){
			case * :
			case * :
			.......
		}
		【2】switch后面是一个()，()中表达式返回的结果是一个等值，这个等值的类型可以为：
		int,byte,short,char,String,枚举类型
		【3】这个()中的等值会依次跟case后面的值进行比较，如果匹配成功，就执行:后面的代码
		【4】为了防止代码的“穿透”效果：在每个分支后面加上一个关键词break，遇到break这个分支就结束了
		【5】类似else的“兜底”“备胎”的分支：default分支
		【6】default分支可以写在任意的位置上，但是如果没有在最后一行，后面必须加上break关键字，
		如果在最后一行的话，break可以省略
		【7】相邻分支逻辑是一样的，那么就可以只保留最后一个分支，上面的都可以省去不写了
		【8】switch分支和if分支区别：
		表达式是等值判断的话--》if ，switch都可以
		如果表达式是区间判断的情况---》if最好
		【9】switch应用场合：就是等值判断，等值的情况比较少的情况下
		*/
	}
}
```






# while循环

```java
public class TestWhile{
	public static void main(String[] args){
		//功能：1+2+3+4+5
		//1.定义变量：
		int num = 1;
		//2.定义一个求和变量，用来接收和：
		int sum = 0;
		
		while(num<=5){
			sum += num;
			num++;
		}
		
		
		//3.输出和
		System.out.println(sum);
	}
}
```
# do whlie 循环
```java
public class TestDoWhile{
	public static void main(String[] args){
		//1+2+3+4+...100
		//while方式:
		/*
		int i = 101;
		int sum = 0;
		while(i<=100){
			sum += i;
			i++;
		}
		System.out.println(i);//101
		System.out.println(sum);//0
		*/
		//do-while方式：
		
		int i = 101;
		int sum = 0;
		do{
			sum += i;
			i++;
		}while(i<=100);//一定要注意写这个分号，否则编译出错
		System.out.println(i);//102
		System.out.println(sum);//101
		/*
		【1】while和do-while的区别:
			while:先判断，再执行
			do-while:先执行，再判断---》至少被执行一次，从第二次开始才进行判断
		【2】什么场合使用do-while:
		
		while(考试是否通过){
			考试；
		}
		---》不合适
		do{
			考试；
		}while(考试是否通过);
		---》合适
		*/
		
	}
}


```

# for 循环
```java
public class TestFor01{
	public static void main(String[] args){
		//1+2+3+..+100
		//while:
		/*int i = 1;
		int sum = 0;
		while(i<=100){
			sum += i;
			i++;
		}
		System.out.println(sum);
		*/
		
		//for:
		int sum = 0;
		int i;
		for(i = 1;i<=100;i++){
			sum += i;
		}
		System.out.println(sum);
		System.out.println(i);
		
		/*
		【1】for的结构：
		for(条件初始化;条件判断;迭代){
			循环体；
		}
		
		【2】i的作用域：作用范围：离变量最近{}  --->可以自己去控制
		【3】for循环格式特别灵活：格式虽然很灵活，但是我们自己写代码的时候不建议灵活着写。
		for(;;){}  -->死循环
		
		int i = 1;
		for(;i<=100;){
			sum += i;
			i++;
		}
		
		【4】死循环：
		for(;;){}
		
		while(true){}
		
		do{
			
		}while(true);
		
		【5】循环分为两大类：
		第一类：当型   while(){}   for(;;){}
		第二类：直到型  do{}while();
		
		【6】以后常用：for循环 
		【7】do-while,while,for循环谁的效率高？  一样高 
		*/
	}
}
```






# break
```java
public class TestFor02{
	public static void main(String[] args){
		//功能：求1-100的和，当和第一次超过300的时候，停止程序
		int sum = 0;
		for(int i=1;i<=100;i++){	
			sum += i;	
			if(sum>300){//当和第一次超过300的时候
				//停止循环
				break;//停止循环
			}
			System.out.println(sum);
		}
		
	}
}
```
**java中的break默认结束最近的一层循环，当然我们可以使用标签使他结束指定的循环**
```java
public class TestFor04{
	public static void main(String[] args){
		outer:
		for(int i=1;i<=100;i++){
			System.out.println(i);
			while(i==36){
				break outer;  
			}
		}
	}
}
```
**添加标签后就可以指定结束循环的位置**

# continue

```java
public class TestFor06{
	public static void main(String[] args){
		//continue:结束本次离它近的循环，继续下一次离他最近的循环
		/*
		for(int i=1;i<=100;i++){	
			if(i= =36){
				continue;//1-100中间没有36
			}
			System.out.println(i);
		}
		*/
		
		for(int i=1;i<=100;i++){	
			while(i= =36){
				System.out.println("------");
				continue; //1-35+死循环
			}
			System.out.println(i);
		}
	}
}
```
### continue带标签的使用
```java
public class TestFor07{
	public static void main(String[] args){
		
		outer:
		for(int i=1;i<=100;i++){	
			while( i= =36){
				continue outer;  //1-100没有36
			}
			System.out.println(i);
		}
	}
}
```

# return
### 结束当前的整个方法
```java
public class TestFor08{
	public static void main(String[] args){
		//return:遇到return结束当前正在执行的方法
		for(int i=1;i<=100;i++){	
			while(i= =36){ 
				return;  
			}
			System.out.println(i);
		}
		
		System.out.println("-----");//return后控制台绝对不会输出这句话
	}
}
```







# 锻炼思维能力
```java
package 循环;

public class Hi {
	public static void main(String[] args) {
		System.out.println("乘法口诀的输出");
		 
		for(int i=1;i<=9;i++) {
			for(int n=1;n<=i;n++) {
				System.out.print(i+"*"+n+"="+i*n+"\t");
			}
				System.out.println();
		}
		
		System.out.println();
		for(int i=9;i>=1;i--) {
			for(int n=1;n<=i;n++) {
				System.out.print(i+"*"+n+"="+i*n+"\t");
			}
				System.out.println();
		}
		
	}
	
}
```






# 数组引入
```java
import java.util.Scanner;
public class TestArray03{
    public static void main(String[] args){
		//功能：键盘录入十个学生的成绩，求和，求平均数：
		//定义一个int类型的数组，长度为10 ：
		int[] scores = new int[10];
		//定义一个求和的变量：
		int sum = 0;
		Scanner sc = new Scanner(System.in);

		for(int i=1;i<=10;i++){//i:控制循环次数
			System.out.print("请录入第"+i+"个学生的成绩：");
			int score = sc.nextInt();
			scores[i-1] = score;
			sum += score;
		}
		
		System.out.println("十个学生的成绩之和为："+sum);
		System.out.println("十个学生的成绩平均数为："+sum/10);
		
		 
		//求第6个学生的成绩： 
		//System.out.println(scores[5]);
		/*
		System.out.println(scores[0]);
		System.out.println(scores[1]);
		System.out.println(scores[2]);
		System.out.println(scores[3]);
		//....
		System.out.println(scores[9]);
		*/
		//将数组中的每个元素进行查看--》数组的遍历：
		//方式1：普通for循环---》正向遍历：
		for(int i=0;i<=9;i++){
			System.out.println("第"+(i+1)+"个学生的成绩为："+scores[i]);
		}
		
		//方式2：增强for循环:
		//对scores数组进行遍历，遍历出来每个元素都用int类型的num接收：
		int count = 0;
		for(int num:scores){
			count++;
			//每次都将num在控制台输出
			System.out.println("第"+count+"个学生的成绩为："+num);
		}
		
		/*
		增强for循环：
		优点：代码简单
		缺点：单纯的增强for循环不能涉及跟索引相关的操作
		*/
		
		//方式3：利用普通for循环： 逆向遍历：
		for(int i=9;i>=0;i--){
			System.out.println("第"+(i+1)+"个学生的成绩为："+scores[i]);
		}
		
	}
}



```

# 数组初始化
## 静态初始化
```java
定义数组同时为数组元素分配内存
int[] arr = {12,13,114};
int[] arr = new int[]{12,13,114};
注意：
1/new int[3]{12,13,114};错误
2/int[] arr
arr={12,13,114}错误
```
## 动态初始化
```java
数组定义与为数组元素分配空间并赋值操作分开
int[] arr;
arr=new int[3];
arr[0]=12;
arr[1]=13;
arr[2]=114;
```
## 默认初始化
```java
int[] arr =new int[3]--->数组内元素已经有分配好的默认值
```
# 数组长度的获取
```java
arr.length;
```







```java

public class TestArray12{
	/*
	1.可变参数：作用提供了一个方法，参数的个数是可变的 ,解决了部分方法的重载问题
	int...num
	double...num
	boolean...num
	
	
	2.可变参数在JDK1.5之后加入的新特性
	3.方法的内部对可变参数的处理跟数组是一样
	4.可变参数和其他数据一起作为形参的时候，可变参数一定要放在最后
	5.我们自己在写代码的时候，建议不要使用可变参数。
	*/
    public static void main(String[] args){
		//method01(10);
		//method01();
		//method01(20,30,40);
		method01(30,40,50,60,70);
		//method01(new int[]{11,22,33,44});
	}
	public static void method01(int num2,int...num){
		System.out.println("-----1");
		for(int i:num){
			System.out.print(i+"\t");
		}
		System.out.println();
		
		System.out.println(num2);
	}
}

```






```java
import java.util.Arrays;
public class TestArray13{
	public static void main(String[] args){
		//给定一个数组：
		int[] arr = {1,3,7,2,4,8};
		//toString:对数组进行遍历查看的，返回的是一个字符串，这个字符串比较好看
		System.out.println(Arrays.toString(arr));
		
		//binarySearch:二分法查找：找出指定数组中的指定元素对应的索引：
		//这个方法的使用前提：一定要查看的是一个有序的数组：
		//sort：排序 -->升序
		Arrays.sort(arr);
		System.out.println(Arrays.toString(arr));
		System.out.println(Arrays.binarySearch(arr,4));
		
		int[] arr2 = {1,3,7,2,4,8};
		//copyOf:完成数组的复制：
		int[] newArr = Arrays.copyOf(arr2,4);
		System.out.println(Arrays.toString(newArr));
		
		//copyOfRange:区间复制：
		int[] newArr2 = Arrays.copyOfRange(arr2,1,4);//[1,4)-->1,2,3位置
		System.out.println(Arrays.toString(newArr2));
		
		//equals:比较两个数组的值是否一样：
		int[] arr3 = {1,3,7,2,4,8};
		int[] arr4 = {1,3,7,2,4,8};
		System.out.println(Arrays.equals(arr3,arr4));//true
		System.out.println(arr3==arr4);//false ==比较左右两侧的值是否相等，比较的是左右的地址值，返回结果一定是false
		
		//fill：数组的填充：
		int[] arr5 = {1,3,7,2,4,8};
		Arrays.fill(arr5,10);
		System.out.println(Arrays.toString(arr5));
	}
}
```
# System里的数组复制
```java
import java.util.Arrays;
public class TestArray14{
	public static void main(String[] args){
		//给一个源数组：
		int[] srcArr = {11,22,33,44,55,66,77,88};
		//给一个目标数组：
		int[] destArr = new int[10];
		
		//复制：
		System.arraycopy(srcArr,1,destArr,3,3);
		//遍历查看目标数组：
		System.out.println(Arrays.toString(destArr));
	}
	
}
```






```java

public class TestArray15{
	public static void main(String[] args){
		//定义一个二维数组：
		int[][] arr = new int[3][];//本质上定义了一个一维数组，长度为3
		
		int[] a1 = {1,2,3};
		arr[0] = a1;
		
		arr[1] = new int[]{4,5,6,7};
		
		arr[2] = new int[]{9,10};
		
		//读取6这个元素：
		//System.out.println(arr[1][2]);
		
		//对二维数组遍历：
		//方式1：外层普通for循环+内层普通for循环：
		for(int i=0;i<arr.length;i++){
			for(int j=0;j<arr[i].length;j++){
				System.out.print(arr[i][j]+"\t");
			}
			System.out.println();
		}
		
		//方式2：外层普通for循环+内层增强for循环：
		for(int i=0;i<arr.length;i++){
			for(int num:arr[i]){
				System.out.print(num+"\t");
			}
			System.out.println();
		}
		
		//方式3：外层增强for循环+内层增强for循环：
		for(int[] a:arr){
			for(int num:a){
				System.out.print(num+"\t");
			}
			System.out.println();
		}
		
		//方式4：外层增强for循环+内层普通for循环：
		for(int[] a:arr){
			for(int i=0;i<a.length;i++){
				System.out.print(a[i]+"\t");
			}
			System.out.println();
		}

	}
}
```
# 数组

**Array ：**

多个相同类型的数据按照一定顺序排列的集合

**数组相关概念：**

数组名、元素、下标或者索引、数组的长度

**数组特点：**

有序排列的

数组本身是引用数据类型的变量

数组的元素既可以是基本数据类型，也可以是引用数据类型

数组长度确定不能修改

**数组分类**：

1、按照维数：一维、二维······

2、按照数组元素类型：基本数据类型元素，引用数据类型元素

## 一维数组的使用：

1、声明和初始化

2、调用指定位置元素

3、获取数组长度

4、遍历数组

5、数组元素默认初始化值

6、数组的内存解析 

```java
1.1静态初始化:数组的初始化和数组元素的赋值操作同时进行
int[] ids ;//声明
ids =new int []{1,5,2,4};
1.2动态初始化:数组的初始化和数组元素的赋值操作分开进行
String []names=new String[4];
//数组一旦初始化完成，其长度就确定

2、调用数组指定位置元素：通过角标调用，从零开始，到数组长度-1结束
names[0]="码帅";

3、获取数组长度，
属性length
names.length;

4、遍历
for(int i=0;i<names.length;i++)
{
    System.out.println(names[0]);
}

5、数组元素的默认初始化值
    整形：0
    浮点型：0.0
    char型：阿克斯马是0。而不是'0'。不是空格
    boolean型:false
    数组元素是引用数据类型：null
int[] arr=new int [4];
for(int i=0;i<arr.length;i++)
{
    System.out.println(arr[i]);
}

6、数组的内存解析
    栈：局部变量
    堆：new出来的结构：对象、数组
```

## 多维数组的使用：

二维数组：一维数组作为另一个一维数组的元素

```java
1、声明和初始化
    静态初始化
int[][]arr=new int[][]{{1,2,3},{4,5},{8,7,5}};
	动态初始化
String[][]arr2=new String[3][2];//行列
String[][]arr2=new String[3][];//只写行也行
    行数必须要有
2、调用指定位置元素
        arr2[0][2];
3、获取数组长度
arr.length结果是行数
arr[0].length//数组的元素也可以利用.length
4、二维数组遍历
    for(int i=0;i<arr.length;i++){
        for(int j=0;j<arr[i].length;i++){
            System.out.println(arr[i][j]);
        }
    }
5、数组元素的默认初始化值
    二维数组分为外层数组元素和内层数组元素
    int [][]arr=new int[4][5]
    外层元素：arr[1]
    内层元素：arr[1][2]
    //----------------------
    int [][]arr=new int[4][3];
	arr[0];		一个地址值
    arr[0][0];	0
    //----------------------
    float [][]arr=new float[4][3];
	arr[0];		一个地址值
    arr[0][0];	0.0
    与一维数组类似，只不过多了外层数组元素的默认值，一个地址值
    //----------------------
    float [][]arr=new float[4][];
	arr[0];		null(未初始化内部元素，引用数据类型就是null)
    arr[0][0];	报错
6、内存结构
       
```

## 数组涉及算法

**1、数组元素的赋值**

**2、求数值型数据**

<u>求最大值、最小、平均、总和</u>

**3、数组的赋值反转查找**

<u>利用数组给数组赋值时直接赋地址值</u>

<u>如果复制就把新数组new出来，给数组元素赋值</u>

**复制不等于赋值**

反转：

```java
for(int i=0,j=arr.length-1;i<j;i++,j--){
    String temp =arr[i];
    arr[i]=arr[j];
    arr[j]=temp;
}
```

线性查找、二分查找：

	线性查找：遍历对比
	
	二分法查找（前提有序）：

```=
int []arr2=new int []{1,2,3,4,5,6,7,8};
int dest=7;
int head=0;//初始首索引
int end =arr.length-1;//初始末索引
while(head<end){
	int middle=(head+end)/2
	if(dest==arr[middle]){
		break;
	}else if(arr[middle]>dest){
		end=middle-1;
	}else{
		head=middle+1;
	}
}
```

**排序**

稳定性：两个记录关键字值相等，但排序后A B先后次序保持不变，则称为稳定

*十大内部排序算法*

**冒泡排序，快速排序**必须掌握

<u>冒泡排序：</u>

n是长度

**外层n-1**：长度减一

**内存n-1-i**：

内部比较，大的靠后或者小的靠后按需交换

<u>快速排序：</u>

## 数组工具类的使用

java.util.Arrays

## 数组中常见的异常

1、数组角标越界

2、空指针异常

2.1、数组没有初始化

2.2、二维只有行没有列，但是用到列了

3、调用数组工具方法，但是数组本身是null，是无法通过null调用方法的，所以报错


## 数组的总结
