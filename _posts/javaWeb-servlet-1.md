---
title: servlet(1)
date: 2017-10-16 18:13:28
tags: [Servlet, 动态网页]
categories: javaWeb
---
<h2>动态网页</h2>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在学习servlet之前我们首先应该知道servlet是干什么的？servlet究竟是什么？<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在了解servlet之前我觉得我们有必要知道动态网页是什么？以及动态网页中浏览器与web服务器([B/S系统架构](http://wangshiyibazhang.club/2017/10/14/C-S%E4%B8%8EB-S%E7%B3%BB%E7%BB%9F%E6%9E%B6%E6%9E%84/))是如何详细交互的？<br/>

<!--more-->
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;动态网页就是在时刻和条件不同的情况下浏览器所获得的网页内容是不同的；与动态HTML页面不同的是，动态网页是在源文件内容改变后在浏览器端显示的动态效果，动态HTML页面是浏览器执行JS程序所呈现的动态效果；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;关于浏览器与web服务器的详细交互过程我在这里画了一个图来解释<br/> ![](http://ox8t0ws1t.bkt.clouddn.com/image/Servlet/%E6%B5%8F%E8%A7%88%E5%99%A8%E4%B8%8Eweb%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%A4%E4%BA%92%E5%9B%BE%E8%AF%A6%E7%BB%86%E8%BF%87%E7%A8%8B%E5%9B%BE.PNG)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;从上图中我们可以看出来动态网页程序的内容是包含两部分的：(1)用一种编程语言编写出的相应的网页程序;(2)一个专门用来执行这个网页程序的模块；我们通常将专门解释网页程序的这种模块称为引擎，如：ASP引擎、JSP引擎、Servlet引擎；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>引擎的作用：</b>在web服务器中引擎直接与浏览器进行交互，引擎同时还翻译动态网页程序的内容提供给浏览器；同时web服务器可以直接可以将静态的HTML文件直接提供给浏览器；当然如果引擎想要与动态网页程序取得联系就得提供相应的API给动态网页程序，这儿的API主要有两个作用：(1)将用户的访问信息传递给网页程序处理，(2)将网页程序处理的结果传递给引擎；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>动态网页程序的作用:</b>网页程序在接收了引擎中传递过来的用户请求信息之后，对服务器端数据库进行相应的操作并将接收数据库操作后所返回的结果。<br/>
	<hr/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;综上所述,我们了解了动态网页以及浏览器与服务器交互的详细过程；我们在上面接触到的一个动态网页程序就是一个servlet；
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;所以Servlet就是实现了一个特殊接口的java类它由具有Servlet引擎的web服务器调用；

<hr/>
ps:以上就是我对servlet的入门的一个理解，以及一些知识的总结，如果有哪位大神有更好的见解希望能与鄙人分享心得，在之后我会将servlet慢慢更出来了的。。。




