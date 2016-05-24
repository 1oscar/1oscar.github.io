---
layout: post
title: "scala笔记(scala详细总结精辟版本)" 
comments: true
share: true
tags: scala
---


1. 运行环境：jvm， 集合面向对象和函数式编程，静态类型编程语言。

2.访问任何java类库并且和java框架互操作。

3.scala作为脚本运行：

```
#!/usr/bin/env scala
```

3.scalac **.scala是将scala代码编译为jvm可以运行的字节码。

4.scala中_即java中的*

5.scala中索引从0开始，但元组是从1开始。

6.val即java中final变量，var即java中非final变量。

7.scala中if/else表达式有值，此值就是跟在if/else后面的表达式的值。

if/else表达式类型以值类型为准，如果是混合类型，则使用超类Any，if

语句无else，当if不满足时，表达式结果为unit类型。相当于if(x>1) 1 else ()

8.scala无for(;;)循环，使用for (x <- 表达式）。for(..)yield最终产生一个新的集合。

9.scala无break和continue，替换：使用Boolean类型控制变量或者使用嵌套函数，从函数中return。
scala无switch，替换：match。

10.

```
定义函数，可以省略返回值类型声明（即无需声明val）。但是递归函数不可省略。声明函数返回类型，可以使你的接口清晰，
建议不要省略返回类型。scala函数参数都是val类型，且不需要声明，也不要重新赋值。类可以加val参数声明。
```

11.闭包：函数中使用了函数外的局部变量，形成了一个闭包。

```
var sum=0
List(1,2,3,4,5).foreach(x => sum+=x)
```

12.private：外部类无法访问内部类的私有成员。
protected：同一包中的其他类无法访问被保护的成员。<br>
13.object定义的成为单例对象，如果类class和单例对象名字一样，则对象为伴生对象，类为伴生类。
伴生对象和类为可以互访其私有成员。单例对象不带参数，类带参数。<br>
14.加上lazy修饰符的val变量称为懒值。<br>
15.覆盖：子类覆盖了父类的具体成员，必须带override修饰符；实现同名的抽象成员，override可选。
未覆盖和实现基类中的成员，禁用override修饰符。<br>
16.显示类型测试：a.isInstanceOf[String]<br>
显示类型转换：a.asInstanceOf[String]
17.各集合关系
![集合关系](http://1oscar.github.io/photos/blogPhotos/scala%E7%AC%94%E8%AE%B0/scala%E7%AC%94%E8%AE%B01.png)

![可变与不可变对应关系](http://1oscar.github.io/photos/blogPhotos/scala%E7%AC%94%E8%AE%B0/scala%E7%AC%94%E8%AE%B02.png)

 
18.定长数组使用Array，长度不可改变；变长数组使用ArrayBuffer。
构造多维数组，使用ofDim或者直接使用for循环来new。示例：

```
val matrix = Array.ofDim[Double](3,4)
matrix（1）（2) = 12.35
或者
val mutl = new Array[Array[Int]](10)
for(i <- 0 until mutl.length)
     mutl(i) = new Array[Int](5)
```

19.列表：
不可变列表：List，可变列表：ListBuffer
List无append，ListBuffer有append，完成后toList即可。
val list1 = List("a") //List是伴生对象，相当于List.apply()
<br>

20.栈和队列，可变与不可变都是Stack和Queue。<br>
21.元组可以使用点，下划线，从1开始索引访问其中元素。<br>

```
val t = (1400,"a", 3.14)
val second = t._2  //引用元祖第二个组元
```

22.异常：

```
scala与java区别：
scala的throw表达式有值的，其值是Nothing类型。
try。。。catch。。。finally表达式有值。无异常，表达式值为try里的，有异常时，
catch里的值。finally里主要是用来关闭文件，套接字，数据库等。
```

23.scala I/O类库:
scala.Console对象用于终端的输入和输出。终端输入有：readLine,readChar,readInt;<br>
终端输出有：print,pringIn,printf

24.java基于共享数据和锁的线程模型，scala是不共享任何数据，依赖消息传递的模型。

```
Actor与并发：
1）设计并发软件，Actor是首选的工具。
2）实现actor方法是继承scala.actors.Actor,重写act方法，start()方法启动。
actor运行时相互独立，或者通过scala.actors.Actor对象的actor方法创建actor，
此时不需要start方法。
3） 发送接收消息
object ScalaTest extends Actor{
     def act(){
          while(true){
               receive{   //receive方法接收消息
                    case msg =>println(msg)  //消息处理的模式匹配（偏函数）
               }
          }
     }
     
     def main(args:Array[String]){
           start()
           this ! "hello"  //使用！发送消息
     }
}
步骤：！发送消息，在actor中等待处理，直到actor调用receive方法，
receive里的模式匹配开始，无匹配成功的消息，则actor消息堵塞，直到收到匹配的消息。
4）还有很多内容。
```

24.GUI编程
使用scala.swing库，提供对java的Swing框架的GUI类的访问。<br>

25.

```
scala和java代码之间传递数据，如果使用的是容器类库，需要转换，
import      scala.collection.JavaConversions._
```





