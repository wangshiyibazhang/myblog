---
title: tomcat
date: 2017-10-04 17:49:13
tags: [tomcat]
categories: javaWeb
---
<style type="text/css">
 img{width:500px;height:300px;border:1px solid;}
</style>
ps:今天学完车闲来无事，突然想起自己在几个月前安装Tomcat时候遇到的坑，跟众君分享下；
<h3>Tomcat的下载与安装</h3>
   
<!--more-->

&nbsp;&nbsp;&nbsp;&nbsp;首先可以去[Apache官网](http://tomcat.apache.org/)找到自己想要下载的版本，![Tomcat下载](http://ox8t0ws1t.bkt.clouddn.com/image/tomcat/installTomcat.PNG)<br/>
注意：zip格式的是免安装版的，exe是安装版的;我框出来的这个是Windows系统下的，然后根据你的系统版本下载相应的文件就行！<br/>
&nbsp;&nbsp;&nbsp;&nbsp;接下来找到你下载好的文件，如果是免安装的，找到目录bin下的startup.bat启动Tomcat，和shutdown.bat关闭Tomcat。如果是安装版的，直接点击exe文件，无脑的下一步就行；![Tomcat启动](http://ox8t0ws1t.bkt.clouddn.com/image/tomcat/Tomcatview.PNG)<br/>
如果你想要测试是否安装成功，打开可视化界面点击start按钮，然后在你的浏览器输入localhost:8080/看到以下界面就说明安装成功;
![installSuccess](http://ox8t0ws1t.bkt.clouddn.com/image/tomcat/Tomcat.PNG)<br/>
<h3>填坑来了</h3>
<ol>
	<li>你要确认你的操作系统上是安装了JDK的</li>
	<li>你要确认你的JDK版本与Tomcat版本是对应的（ps：当初我在CSDN社区下的Tomcat5，JDK版本是1.8的结果部署的时候就蒙圈了。。。）</li>
	<li>在你无脑下一步的时候，最好将你的安装路径不要放在C盘下，因为现在很多版本的win10系统下的C盘默认是不支持文件写入的，在你部署你的web应用的时候，你的资源将无法写入，所以为了方便起见你还是将它不要放在C盘下</li>
<ol>
<hr/>

以上就是鄙人在安装Tomcat的时候遇到的一些问题，希望能与众君共勉，有什么不对的地方还请众君批评指正！