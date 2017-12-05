---
title: servlet(3)-ServletContext和Response
date: 2017-10-29 17:25:12
tags: [servlet, response, application]
categories: javaWeb
---
<h3>ServletContext对象</h3>
<h4>获取方法</h4>
```
//获取ServletContext方法1
ServletContext context=this.getServletConfig().getServletContext();
//获取ServletContext方法2
context = this.getServletContext();
```
<!--more-->

<h4>作用域范围</h4>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在一个web应用程序中，多个Servlet共享一个ServletContext对象，因此也可以将该对象称为application对象；如果要使某个web应用中的ServletContext.getContext方法返回其他web应用中的ServletContext对象，就需要在服务器配置文件server.xml中，将<Context/>元素的crossContext属性的值置为true。
<h4>访问资源文件</h4>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ServletContext接口中定义了两个获取内部文件的方法：getResourse和getResourceAsStream<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getResource方法</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;该方法会映射到某个资源文件上的URL对象，传递给该方法的参数必须是以"/"开头，代表当前web应用的根目录，返回值是一个String对象；<br/>

```
//获取配置文件的绝对路径
String path =this.getServletContext().getRealPath("WEB-INF/classes/db.properties");   	
String filename= path.substring(path.lastIndexOf("\\")+1);
```
<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getResourceAsStream方法</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;该方法参数的传递和getResoure方法的相同，但是他将连接到某个资源的InputStream对象上面，返回一个InputStream流，可直接用该流读取数据;

```
InputStream in =this.getServletContext().getResourceAsStream("WEB-INF/classes/db.properties"); 
//读取配置文件的方法
Properties pros = new Properties();
pros.load(in);
```
<hr/>
<h3>HttpServletResponse</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Response是专门用来给用户会送服务器对于用户请求的响应的<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ServletResponse是Servlet引擎创建的一个接口，HttpServletResponse是他的子接口用于Http协议，操作Http相关的数据。
<h4>产生状态响应行和构建响应消息头</h4>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Response对象的setStatus方法可以设置响应消息的状态码，并生成响应的响应行；addHeader和setHeader方法用来构想响应消息头

```
//指定浏览器查UTF-8码表
response.setHeader("content-type","text/html;charset=UTF-8");
//向浏览器发送缓存请求头，并设置缓存时间
response.setDateHeader("expires", System.currentTimeMillis()+1000*3600);
```
<h4>设置字符编码</h4>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;可以通过Response对象中的相应的方法通知内容是以哪个字符码表写入硬盘以及浏览器以哪种编码获取内容，以防中文乱码问题；<br/>
可以通过以下几种方式：

```
//指定response码表为UTF-8
response.setCharacterEncoding("UTF-8");
//指定浏览器查UTF-8码表
response.setHeader("content-type","text/html;charset=UTF-8");

//以下代码指定浏览器查UTF-8码表的同时也设定response的码表为UTF-8,等同于上两行代码
response.setContentType("text/html;charset=UTF-8");

//通过html的<meta >标签写响应头告诉浏览器查UTF-8码表
out.write("<meta http-equiv='content-type' content='text/html;charset=UTF-8'>".getBytes())
```
<h4>响应正文的创建</h4>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ServletResponse是Servlet程序与Servlet引擎的通信接口，可以将响应正文传递给引擎然后引擎再交由浏览器显示，对于大量数据的传输，通过IO流进行传递，Response提供了字节流OutputStream和字符流PrintWriter进行正文的输出。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getOutputStream方法</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;返回值为OutputStream对象，可以直接输出字节数组中的二进制数据，可以用来输出图片、音乐等。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getWriter方法</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;返回值为PrintWriter对象，只能用于输出纯文本网页文档<br/>
<b>对于以上两个流输出之前首先应该设置响应的字符编码，且二者不可同时存在！</b>



