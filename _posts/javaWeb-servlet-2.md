---
title: servlet(2)
date: 2017-10-21 18:49:36
tags: [servlet, javaWeb]
categories: javaWeb
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我之前整理的[servlet简介](http://wangshiyibazhang.club/2017/10/16/javaWeb-servlet-1/#more)有介绍什么是servlet，以及再学习servlet前应该了解的一些知识，今天我将整理一些稍微深入点的servlet以及我的见解

<!--more-->
<h3>servlet在web应用中的位置</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们在访问一个网页时，其实是在访问web服务器主机上已经部署好的一个web应用，至于web应用内部是如何储存一个servlet的我在这里画了一张图<br/>
![servlet在web应用中的位置图](http://ox8t0ws1t.bkt.clouddn.com/image/Servlet/servlet%E5%9C%A8web%E5%BA%94%E7%94%A8%E4%B8%AD%E7%9A%84%E4%BD%8D%E7%BD%AE.PNG)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先我们的web应用是在服务器目录下的webapps中，在web应用目录下我们可以直接装一些静态文件或者静态文件夹，其次在WEB-INF目录下又提供了专门装java类的文件夹和类所用的jar包文件夹以及web应用的配置文件；一个个实现了servlet接口的java类也就是一个个的servlet都是装在classes目录下的。
<h3>servlet的运行过程</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在servlet中有init(),service(),destory()几个主要的周期方法，这几个方法是在什么情况下调用的我画了一张图来说明：<br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/Servlet/servlet%E8%BF%90%E8%A1%8C%E8%BF%87%E7%A8%8B.PNG)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;客户端浏览器在首次访问一个web应用的时候，servlet引擎会装载并创建一个servlet对象，然后调用该对象的init()方法初始化该对象(<font color="red">在初始化的时候servlet的时候servletAPI定义了有ServletConfig参数和无参的init()方法供调用</font>)，接着就调用service()方法(<font color="red">在servlet存活的这个周期中，浏览器发送的请求和服务器回送的响应都由service()方法处理，即service()方法是多次被调用的</font>)，最后在浏览器和服务器交互完毕之后，又会调用destory()方法，关闭流和清理内存中含有的交互过程产生的垃圾等。<br/>
<h4>init()方法</h4>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在一次交互过程中，初始化方法init()会在创建对象后调用，但是如果已经存在servlet对象就不会调用该方法；destory()方法只会在断开连接之前调用一次。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在调用初始化方法init()时，servlet引擎提供的ServletConfig对象可以作为该方法的参数传递，ServletConfig对象可以封装一些servlet的配置信息，比如：servlet使用的数据库、字符码表等的配置文件都没必要写死在程序中，这时我们就可以通过ServletConfig对象配置给servlet。
<h4>service()方法</h4>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;service()方法是servlet中最核心的方法，它用来直接处理用户的请求和给用户回送响应，HttpServlet类在该方法中提供了两个参数HttpServletResquest request和HttpServletResponse response，分别用来装用户请求和回送给用户的相应。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;无论客户端以哪种方式发送请求servlet引擎最终都会调用service()方法处理该请求，所以说service()方法是所有请求的总入口；通常情况下servlet处理的请求无非就是GET和POST两种方式，所以我们无需覆盖整个service方法，只需覆盖其中的doGet()和doPost()方法即可。

<hr/>
ps:以上就是我整理以及总结的servlet相关的内容，在之后我还会继续更新该方面的知识。。。














