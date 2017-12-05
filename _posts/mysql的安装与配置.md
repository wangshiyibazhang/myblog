---
title: mysql的安装与配置
date: 2017-11-08 13:43:47
tags: [mysql, sql]
categories: 数据库
---
ps:在大二学习数据库的时候用的是SQL Server，但是它比较适合用于支持大中型系统的开发，对于我们学习而言，MYSQL短小精悍，容易上手，操作简单，免费供用的。相对其它数据库有特色又实用的语法多一些。

<!--more-->
<h2>mysql的安装</h2>
<ol>
	<li>mysql的[下载](https://dev.mysql.com/downloads/installer/),点击“下载”，根据自己的电脑的型号下载</li>
	<li>点击应用程序，选择“安装”，或者将压缩包打开后运行其中的“setup.exe”文件</li>
	<li>可以选择默认安装或者自定义安装都行，安装完成后进入配置界面</li>
</ol>
<h2>mysql的配置</h2>
<ol>
	<li>选择配置方式，"Detailed Configuration（手动精确配置）"</li>
	<li>选择服务器类型，"Developer Machine（开发测试类，mysql占用很少资源）"、"Server Machine（服务器类型，mysql占用较多资源）"、"Dedicated MySQL Server Machine（专门的数据库服务器，mysql占用所有可用资源）"，在这里我们选择开发测试类</li>
	<li>选择择mysql数据库的大致用途，"Multifunctional Database（通用多功能型）"、</li>
<li>之后的都选择默认就行（用户名和密码的设置最好简单易记）</li>
<li>确认设置无误，按"Execute"使设置生效，即完成MYSQL的安装和配置。</li>
</ol>
<h2>注意事项</h2>
<ul>
<li>在配置字符集的时候，由于我们经常会在数据库中对中文字符进行操作，为了防止乱码我们应该将字符集设置成utf8，如下所示<br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/mysql/mysql%E5%AE%89%E8%A3%85%E6%97%B6%E7%9A%84%E5%AD%97%E7%AC%A6%E9%85%8D%E7%BD%AE.PNG)</li>
<li>设置完毕，按"Finish"后有一个比较常见的错误，就是不能"Start service"，一般出现在以前有安装mysql的服务器上，解决的办法，先保证以前安装的mysql服务器彻底卸载掉了；不行的话，检查是否按上面一步所说，之前的密码是否有修改，照上面的操作；如果依然不行，将mysql安装目录下的data文件夹备份，然后删除，在安装完成后，将安装生成的 data文件夹删除，备份的data文件夹移回来，再重启mysql服务就可以了，这种情况下，可能需要将数据库检查一下，然后修复一次，防止数据出错。</li>
<li>配置完成且确认服务器已经启动后可以在dos窗口测试一下，使用mysql -u yourname -p yourpassword命令登录，登录后使用\s查看详细信息<br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/mysql/mysql%E7%99%BB%E5%BD%95.PNG)<br/><br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/mysql/mysql%E5%AE%89%E8%A3%85%E6%88%90%E5%8A%9F%E6%97%B6%E7%9A%84%E9%85%8D%E7%BD%AE%E4%BF%A1%E6%81%AF.PNG)</li>
<li>插入和输出数据时的乱码问题，在Windows命令行中使用insert和select语句的时候会出现中文乱码问题，这是因为我们在doc窗口输入的中文是以gb2312码表输入的而mysql中的字符集却是utf-8码表，所以不同码表就会出现乱码问题，因此我们可以针对当前的dos窗口设置字符码表，我们在dos窗口输入show variables like 'chara%'时就会看到所有字符集相关设置，如图<br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/mysql/doc%E7%AA%97%E5%8F%A3%E6%9C%AA%E8%AE%BE%E7%BD%AE%E6%88%90%E5%8A%9F%E7%9A%84%E5%AD%97%E7%AC%A6.PNG)<br/>在这里我们使用set character_set_client=gb2312;命令让客户端以gb2312码表输入，同时 用 set character_set_results=gb2312;在dos窗口以gb2312码表显示结果集，如图<br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/mysql/doc%E7%AA%97%E5%8F%A3%E8%AE%BE%E7%BD%AE%E6%88%90%E5%8A%9F%E7%9A%84%E5%AD%97%E7%AC%A6.PNG)<br/>
<font color="red">以上设置字符码表的方式只针对于当前的dos窗口有用，如果想永久有效就需要将mysql安装目录下的my.ini文件中的客户端字符设置为gb2312如下图所示
</font><br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/mysql/%E6%B0%B8%E4%B9%85%E8%AE%BE%E7%BD%AE%E5%AD%97%E7%AC%A6%E7%A0%81%E8%A1%A8.PNG)
</li>
</ul>