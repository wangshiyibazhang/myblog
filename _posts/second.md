---
title: 首战告捷
date: 2017-09-27 19:08:29
tags: [github, npm, next]
categories: 技术
copyright: true
---
&nbsp;&nbsp;&nbsp;现在基本工作搭建完了，不过域名还没有买，好多插件没有安装，原谅小菜鸡的沾沾自喜。。。嘻嘻。。。(<font color=red face="黑体">以下是本人搭建时碰到的一些细节</font>)
<h1>搭建基本个人博客的一些问题简述</h1>
&nbsp;&nbsp;&nbsp; <font color=#0099ff face="黑体">希望与各位看官共勉</font>
<h3>搭建blog的基本步骤</h3>
<!--more-->
<ol>
	<li>github的注册，这个网上有很多教程,也都很详细我就不详细介绍了</li>
	<li>Node.js 的安装和准备</li>
	<li>hexo的安装和相关配置</li>
	<li>Hexo与github page 联系</li>
</ol>
  ---
<font size="4" face="黑体">以上步骤网上都附上了很详细的教程,而且大神的教程也都很详细。。</font>
  ---
**在这里我说一下我遇到的比较一些典型的问题**

>>首先在“npm install”的时候一定要确认在最初的hexo文件下面还有有一个hexo文件夹，否则就会报错，也可以直接在“npm install”后面添加hexo，即“npm install hexo”
   ---
>>在你体验你的hexo的时候，即hexo g -->hexo s 之后，你最好确认你的4000端口是没有被占用的，完了就是github与hexo的联系
  ---
>>接下来就是再配置主题时的一些问题
<ul>
	<li><font color=red face="黑体">一定注意站点_config.yml(hexo目录下)和主题的_config.yml(themes/[theme name]/下)的区分</font></li>
	<li>一般站点配置文件在实现github和hexo连接后，基本不需要大的改动</li>
	<li>当你在部署时出现很多有关于部署文件的时候你可以直接，将根目录下的.deploy_git文件删除重新"hexo deploy"</li>
	<li>主题的选择自己可以去网上搜下载完之后直接放在你的themes目录下，同时不要忘了在站点目录下更改你的主题配置</li>
	<li>接下来就是你的主题的配置
```
    menu:
  home: /
  categories: /categories
  about: /about
  #archives: 归档
  tags: /tags
  #sitemap: 站点地图
  #commonweal: 公益404
``` 
在menu下的每个标签后面都跟的相应的地址home:/ 就是本页地址
   </li>
	<li>在进行上一步的时候你首先要确保你的hexo/source/下有相应的文件夹和md文件，至于文件夹的创建可以直接在dos窗口创建，也可以自己创建</li>
	<li>至于md文件的编辑用markdown编辑器就可以,Markdown是兼容html语法的，所以我编辑的时候都是用html中的标签</li>
	<li>然后就是编辑你的博客，在这里我用的是markdown编辑器</li>
</ul>
 ---
>以上就是鄙人的浅见，欢迎分享心得！
