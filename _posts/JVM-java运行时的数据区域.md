---
title: java运行时的数据区域和对象的访问
date: 2017-11-27 21:44:26
tags: [jvm, heap, stack]
categories: JVM
---
<h2>运行时的数据区域</h2>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;每个java程序的运行都会需要一定的内存来支持，java虚拟机在执行java程序的时候将内存分为以下几个数据区域。<br/>
![](http://ox8t0ws1t.bkt.clouddn.com/image/JVM/%E8%BF%90%E8%A1%8C%E6%97%B6%E7%9A%84%E6%95%B0%E6%8D%AE%E5%8C%BA%E5%9F%9F.PNG)<br/>

<!--more-->
<h3>1.程序计数器</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;程序计数器是指当前线程所执行的字节码的行号指示器。（占很小的一部分储存空间）<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们知道在多线程的执行是轮流分配处理器的执行时间进行的，并且每个处理器只支持一个线程中的指令，为了使程序在线程切换后能准确的找到上次线程所执行的地方，jvm会给每个线程单独的分配一个计数器，且互不影响，这种内存区域是归线程所私有的。
<h3>2.虚拟机栈</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;虚拟机栈是描述java方法执行时的内部储存模型：即方法在执行的时候就会同时创建一个栈桢，用来储存局部变量表、操作数栈、动态链接、方法出口等信息的；方法的调用过程就是入栈出栈的过程。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们通常所讲的“栈”，就是指虚拟机栈，再进一步细化就是虚拟机栈中的局部变量表。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;局部变量表中所存放的便是基本数据类型和对象总体的引用，一个字节码地址所需的空间在变异的时候就已经分配好了。
<h3>3.本地方法栈（Native Method Stack）</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;和虚拟机栈类似，虚拟机规范对本地方法栈中的各数据要求比较宽松，一般情况下，具体虚拟机可自由实现它。<br/>
<ul>区别：
	<li>Native Method Stack（本地方法栈）：执行本地方法服务</li>
	<li>虚拟机栈：执行java方法服务</li>
</ul>
<h3>4.堆（heap）</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;堆是专门用于存放对象实例以及数组的。
<ol>
	<li>JVM中内存最大的一块</li>
	<li>所有线程共享</li>
	<li>虚拟机启动时创建</li>
	<li>垃圾回收器主要的作用对象，又叫“GC堆”</li>
	<li>在内存中还有自己的内存分配方式，只是为了更方便的垃圾回收</li>
	<li>不需要连续内存进行储存，可选择固定大小也可进行扩展</li>
</ol>
<h3>5.方法区</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法区类似于堆，用于存放Class相关的信息，如类名、访问修饰符、常量池、字段描述、方法描述等。在java虚拟机规范中将方法区描述为堆的一个逻辑部分，但事实上它又称为Non-Heap（非堆）。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;该区域很少进行垃圾回收，但也并非是数据进入该区域就会永久存在（“永久代”），该区域的垃圾回收主要针对常量池回收和堆类型的卸载。
<h3>6.常量池</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;常量池属于方法区，用来存放编译期生成的各种字面量和符号的引用；这些内容在类加载后放在运行时常量池当中。
<h2>对象的访问</h2>

```
Object boj = new Object();
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Object obj 将会反应到虚拟机栈中的本地变量表里并作为一个引用类型（reference）。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;new Object会反应到堆中，形成了一块储存了Object类型所有实例数据的结构内存；且在堆中还应存放了提供此对象的类型数据的地址信息，具体信息存放在方法区中。<br/>

---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;栈中引用类型对具体对象的访问主要有两种形式：
<ol>
	<li>句柄访问：在java堆中专门会分配一块用来储存对象具体数据与数据类型的指向地址的内存，该内存就叫句柄池。<br/>
栈中的引用储存的就是用来访问句柄池的地址。<br/>
![](http://ox8t0ws1t.bkt.clouddn.com/image/JVM/%E5%8F%A5%E6%9F%84%E6%B1%A0%E8%AE%BF%E9%97%AE.PNG)
优点：栈引用储存稳定的句柄地址，对象被移动时，会改变句柄中的实例数据指针无需改变栈引用。
	</li>
	<li>直接访问：栈中引用直接储存对象地址<br/>
	![](http://ox8t0ws1t.bkt.clouddn.com/image/JVM/%E7%9B%B4%E6%8E%A5%E8%AE%BF%E9%97%AE.PNG)
优点：访问速度快
	</li>
</ol>
注意：我们通常所使用的sun公司的虚拟机都使用的是直接访问。

---
<b>本地方法（Native Method）：</b>就是一个java调用非java代码的接口。该方法的实现由非java语言实现，比如C。这个特征并非java所特有，很多其它的编程语言都有这一机制，比如在C＋＋中，你可以用extern "C"告知C＋＋编译器去调用一个C的函数；主要用于与外界环境的交互。
























