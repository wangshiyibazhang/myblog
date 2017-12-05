---
title: 'servlet(4)-Rrequest,Session和Cookie'
date: 2017-11-01 17:21:18
tags: [HttpServletRequest, Session, Cookie, Servlet]
categories: javaWeb
---
<h2>HttpServletRequest对象</h2>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Servlet API中定义了一个专门用来获取用户请求信息的接口ServletRequest接口，可以通过该对象中的方法获取用户请求信息等；HttpServletRequest接口是ServletRequest接口的子接口，用于封装HTTP有关的请求消息，支持Cookie和Session跟踪；该对象是service方法中一参数的方式传递的，当调用service、doPost或doGet方法时该对象就被创建了<br/>

<!--more-->
<h3>获取请求行相关信息</h3>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getMethod</b>方法，返回请求方式(GET或POST)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getContextPath</b>方法，返回请求所属的URL的路径，返回值就是当前web应用根目录；
<h3>获取网络连接信息</h3>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getRemoteAddr</b>方法，返回请求客户机的IP地址<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getScheme</b>方法，返回请求的协议名，如：HTTP、HTTPS等<br/>
<h3>获取请求参数和实体内容</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;通过获取请求参数的一些方法可以获取客户端通过URL地址中传过来的附加信息，还有在表单中以“hidden”形式的input输入项传过来的值；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getParameter</b>方法，通过指定名称的参数，获取对应的值，如果指定的名称对应的值有多个，则返回第一个值<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getParameterValues</b>方法，返回多个具有相同名称参数所对应的值<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getInputStream</b>方法，获取HTTP消息中的实体内容，返回一个字节流ServletInputStream<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getReader</b>方法，只能获取文档形式的实体内容，返回值为BufferReader输入流<br/>
<h3>通过设置属性传递信息</h3>
&nbsp;&nbsp;&nbsp;&nbsp;<b>setAttribute</b>方法，该方法提供两个参数，第一个参数为所传对象的引用，第二个为所传对象的实体，通过该方法可以将一个对象封装在ServletRequest对象中<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getAttribute</b>方法，该方法的参数可以通过setAttribute方法的第一个参数获得，通过ServletRequest对象中所存的对象引用获取相应的对象；
<h3>request中乱码问题</h3>

```
	//post乱码问题
	private void test1(HttpServletRequest request) throws UnsupportedEncodingException{
		//设置和浏览器一样的码表，该设置只对post请求有用
		request.setCharacterEncoding("UTF-8"); 
	    String username = request.getParameter("username");
	    System.out.println(username);
	}

	//get乱码问题,获取编码后手动转换
	private void test2(HttpServletRequest request) throws UnsupportedEncodingException{
		
		String username =request.getParameter("username");
	    username=new String(username.getBytes("iso8859-1"),"UTF-8");
	    System.out.println(username);
	     
	}
```
<h2>Cookie</h2>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cookie是一种在客户端保持HTTP状态信息的技术，因为HTTP协议是无状态的，与服务器连接完毕之后，就会立马断开，当服务器与客户机需要再次连接的时候，就无法进行相应的连接了，所以可以采用Cookie这种技术弥补这种不足；<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="red">当服务器与用户进行连接时，response就会给客户机浏览器颁发一个Cookie用来记录此次连接，当需要再次连接的时候只需在客户端获取Cookie进行验证，就可以实现会话的跟踪；</font><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cookie最先是由服务器发出的，对于是否发送Cookie和发送的具体内容都是由服务器决定的；一个Cookie至少标识一种信息，需要有标识信息的名称和值；一个web站点可以给浏览器发送多个Cookie；浏览器一般允许存放300个Cookie，一个站点只允许存放20个。<br/>
<h3>Cookie对象的创建及其相应的属性</h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Servlet API 中提供了Cookie的构造方法，public Cookie(String name,String value)，可以根据提供的构造方法创建一个Cookie，删除该Cookie的时候只需构建同名Cookie调用setMaxAge方法并将值设置为0即可<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getName</b>方法，返回Cookie的名称；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>setValue和getValue</b>方法，设置和返回Cookie的值<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>setMaxAge和getMaxAge</b>方法，该方法用于设置Cookie在浏览器客户机上的保存时间，其中值为秒数，当值为0秒时则删除这个Cookie；当getMaxAge值为正数时，则该Cookie存在与硬盘上，对该客户机的所有浏览器进程都有效，直到过期；当getMaxAge值为-1时，该Cookie则保存在收留他的浏览器进程中，而且只对该浏览器有效；
<br/>&nbsp;&nbsp;&nbsp;&nbsp;<b>setPath</b>方法，如果没有设置该方法的值得时候，则只对当前访问路径及其子目录有效，如果想对整个web站点中的目录都有效可将该值设置为"/"，或者当前web站点根目录；<br/>
以下是一个简单的Cookie案例：

```
//记录并返回用户上次访问网站的时间
public class cookieDemo1 extends HttpServlet {
	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setCharacterEncoding("UTF-8");
		response.setContentType("text/html;charset=UTF-8");
		
		PrintWriter out =response.getWriter();
		out.print("<a href=/web03/servlet/cookieDemo2?id=1>清除上次访问时间</a>");
		out.print("您上次访问的时间是：");

		//获得用户访问时间
		Cookie cookies[] =request.getCookies();
		for(int i=0;cookies!=null&&i<cookies.length;i++){
			if(cookies[i].getName().equals("lastAccessTime")){
				long value = Long.parseLong(cookies[i].getValue());//获取用户上次访问时间
				Date date = new Date(value);
				String time =date.toLocaleString();
				out.print(time);
			}
		}
				
		//给用户回送最新访问时间
		Cookie cookie = new Cookie("lastAccessTime",System.currentTimeMillis()+"");
		cookie.setMaxAge(1*30*24*3600);
		cookie.setPath("/web03");
		response.addCookie(cookie);
	}
}

//清除用户上次访问网站的时间
public class cookieDemo2 extends HttpServlet {
	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		//创建一个新的cookie设置与要清除的cookie相同路径，相同名字
		Cookie cookie = new Cookie("lastAccessTime",System.currentTimeMillis()+"");
		cookie.setMaxAge(0);
		cookie.setPath("/web03");
		response.addCookie(cookie);
	}

	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

	}

}

```
<h2>HttpSession</h2>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cookie是在客户端保持HTTP状态信息的一种技术，Session是服务器端保存HTTP状态信息的一种技术；一个客户端在服务器端享有一个独有的Session。<br/>
<h3>Session的创建及响应过程：</h3>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;由于创建Session对象会消耗内存资源，<font color="red">web服务器不会再浏览器访问的时候就创建该对象，只有在客户端访问某个特殊的Servlet程序时，并且该程序决定于客户端开启一个会话时，web服务器才会创建一个与该客户端对应的Session对象，</font>并为这个对象分配一个独一无二的会话标识号(SessionID)，然后再服务器产生响应的时候将该会话标识号传给客户端，客户端只需要记住该会话标识号，再后续访问的时候只需要将这个会话标识号传给服务器，然后服务器就会得知是哪个客户端发出的然后找到响应的Session对象。<br/>
在HttpServletRequest对象中提供了创建session对象的方法:getSession；该方法可以传递Boolean类型的参数，当值为false不创建新的Session对象，返回null；当值为true时可以省略该值，会创建一个新的session对象
<h3>Session的摧毁：</h3>Session对象并不会在浏览器关闭的时候就摧毁，Session实在一定的时间类，浏览器再没有发出请求，web服务器就会认为客户端已经停止了活动，然后就会结束此次会话，Session对象也就会变成垃圾等待回收。<br/>
指定的摧毁时间可以在服务器目录\conf\web.xml文件中的以下字段配置：<br/>

```
<session-config>
	<session-timeout>10<session-timeout>
</session-config>
```
10代表十分钟，如果该值为0或者负数则永不超时。
<h3>Session对象的方法</h3>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getId</b>方法，返回当前Session对象的会话标识号<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getServletContext</b>方法，返回当前web应用所属的ServletContext对象<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>isNew</b>方法，该方法用于检查Session对象是否是新建的，如果是则返回true，否则返回false；该方法内部实现是服务器通过检查SessionID是否相同或是否存在，而返回true或者false<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>setAttribute</b>方法，该方法用于将对象通过关联的名称储存在Session对象中，储存方式类似于Map集合的存值方法；因为其内部通过Map集合来实现对象的储存，要删除原来的Session对象时，只需要将创建同名Session对象，并将值设为null<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<b>getAttribute</b>方法，通过setAttribute方法中的关联名称，获取响应对象



















