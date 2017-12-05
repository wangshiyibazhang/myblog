---
title: next
date: 2017-09-29 09:18:50
tags: [next, github]
categories: 技术
copyright: true
---
<h2>next主题</h2>
>之前就有道友说next主题是个让人又爱又恨的主题，在本人的亲历亲为下，暂时是体会到next主题较之其他主题的好处：关于添加各中插件，我就说我自己再添加评论系统的时候吧，虽然我现在的那个版面效果有点瑕疵，
<!--more-->

<ul>
	<li>
	我的next的评论是添加的 [youyan](http://www.uyan.cc),在官网注册  
	</li>
	<li>要实现留言板，你就的新建一个page，
``` 
    hexo new page "留言板name"
```
别忘了在主题的_config.yml中留言板，同时也要在zh-Hans中也要进行相应的配置
  </li>
	<li>记得将你的主题下的_config.yml文件中的youyan: uid配置好，这里的uid就是代码块中uid后面的一串数字</li>
	<li>复制youyan提供的代码块，放在你的留言板中的index.md文件正文中，记得添加一个comments: true</li>
	<li>接下来hexo d -g就可以了</li>
</ul>

next主题下的配置真心省心好多，有木有。。。
