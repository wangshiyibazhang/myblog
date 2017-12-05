---
title: JDBC
date: 2017-11-09 19:18:45
tags: [JDBC, mysql, java]
categories: 数据库
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;数据库可以帮我们方便的组织、储存和管理数据；我们在开发过程中也会操作大量的数据，通过单独的操作数据库会带来很大的不便，因此sun公司提供了一套专门用于执行SQL语句的API 即JDBC。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在通过java程序操作数据库的时候最好是确定已经你已经创建了响应的数据库和表；<br/>

<!--more-->
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在这里我将使用以下数据库和表：<br/>

```
create database db;
use db;
create table student(
	id int primary key,
	name varchar(40) not null,
	age int,
	Sdept varchar(40)
	);
insert into student(id,name,age,Sdept) values("1","aaa","20","AAA");
insert into student(id,name,age,Sdept) values("2","bbb","21","BBB");	
```
---
```
package JDBC;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ResourceBundle;

public class JdbcTest {

	private static String className;
	private static String url;
	private static String user;
	private static String password;
	/*
	 * 通过静态代码块读取数据库配置文件中的信息
	 */
	static{
		ResourceBundle rb = ResourceBundle.getBundle("my");
		className = rb.getString("className");
		url = rb.getString("url");
		user = rb.getString("user");
		password = rb.getString("password");
	}
	
	public static void Updata(){
		Connection conn = null;
		Statement st1 = null;
		PreparedStatement st2 = null;
		ResultSet rs = null;
		try {
			//获取数据库驱动
			Class.forName(className);
			System.out.println("数据库驱动成功！");
			//连接数据库
			conn = DriverManager.getConnection(url,user,password);
			System.out.println("数据库连接成功");
			//创建一个数据操作类
			st = conn.createStatement();
			//查询数据
			String sql = "select * from student";
			//获取结果集
			rs = st.executeQuery(sql);
			//遍历结果集
			while(rs.next()){
				System.out.println(rs.getInt("id"));
				System.out.println(rs.getString("name"));
				System.out.println(rs.getInt("age"));
				System.out.println(rs.getString("Sdept"));
				
			}
			/*
			//插入数据
			String insert = "INSERT INTO Student(id,name,age,Sdept) VALUES(?,?,?,?)";
			st2 = conn.prepareStatement(insert);
			st2.setInt(1,3);
			st2.setString(2, "ccc");
			st2.setInt(3,19);
			st2.setString(4,"CCC");
			int num = st2.executeUpdate();
			if(num>0)System.out.println("插入成功！");
			*/
		} catch (ClassNotFoundException e) {
			System.err.println("数据库驱动失败！");
			e.printStackTrace();
		} catch (SQLException e) {
			System.err.println("数据库连接失败！");
			e.printStackTrace();
		}finally{
			
			/*
			 	从小到大，依次关闭与数据库所有连接，并释放内存
			 */
			 
			if(rs!=null){
				try {
					rs.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
			rs=null;
			if(st!=null){
				try {
					st.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
			st=null;
			if(conn!=null){
				try {
					conn.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
			conn=null;
		}
	}
}
```
配置文件是：my.properties<br/>

```
className=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/db
user=root
password=root
```
<font size="5"><b>注意事项：</b></font>
<ol>
	<li>创建驱动的时候有两种方式：<br/>
      DriverManager.registerDriver(new com.mysql.jdbc.Driver());<br/>
	  Class.forName("com.mysql.jdbc.Driver");<br/>
	创建驱动的时候务必使用反射技术，即第二种方式，因为在Driver类的源码中有段静态代码域就已经new 了一个驱动，如果使用第一种方式就会出现两次驱动的情况；</li>
	<li>在DriverManager类中重构了获取Connection对象的方法，在传值的时候，可以通过URL参数的方式直接传递，但通常都是直接按三个方式传递，getConnection(String url, String user, String password)</li>
	<li>在开发过程中数据库的驱动，以及配置文件的加载都只需要执行一次就够了，所以我们可以将其放置在静态代码块中执行</li>
	<li>在创建链接、获取Statement对象以及结果集之后，要确保将链接关闭；按顺序关，以防万一，可以直接在finally块中关闭，且为了防止出现空指针异常，要关闭不为空的连接所以就应当先进行判断</li>
	<li>在开发过程中导包的时候，务必导入sun公司API中的响应的包，即java.sql和javax.sql，中的否则在我们使用其他的数据库的时候程序 就跑不了了</li>
	<li>Statement对象中，查询数据最好使用executeQuery方法，虽然execute方法也支持，但是该方法返回值是一个Boolean对象，遍历结果的时候还要进行判断，使代码过于繁琐</li>
	<li>在以上程序我使用的是Statement对象执行SQL语句，但是实际开发中最好使用PreparedStatement对象</li>
	<li>Statement和PreparedStatement的区别：<br/>
	a.PreparedStatement是Statement的孩子<br/>
	b.PreparedStatement内部实现了转义sql语句，防止sql的注入问题<br/>
	c.PreparedStatement会对sql语句进行预编译，以减轻数据库服务器的压力</li>
</ol>
