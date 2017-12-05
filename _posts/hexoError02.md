---
title: hexoError02
date: 2017-10-26 15:44:19
tags: [hexo, npm, blog]
categories: 技术
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;因为系统不好用，所以刚刚重装了系统，因此hexo我也就重新配置了一遍，感觉第二遍搭完，好多心得体会(偷笑);<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我之前搭建的时候就简述了一下搭建流程以及注意事项[点击这里](http://wangshiyibazhang.club/2017/09/27/second/)查看，现在我再简述下遇到的另外的一些问题：<br/>

<!--more-->
<h3>npm install -g hexo-cli </h3>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在执行这一步的时候确保你得终端是安装了node.js和npm以及git，可以通过以下指令查看<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![](http://ox8t0ws1t.bkt.clouddn.com/image/hexo/NpmNodeGIT.PNG)<br/>
然后就执行hexo install -g hexo-cli命令，可是再执行该命令的时候报了如下错误

```
H:\blog>npm install -g hexo-cli
npm ERR! Windows_NT 10.0.10240
npm ERR! argv "C:\\Program Files\\nodejs\\node.exe" "C:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install" "-g" "hexo-cli"
npm ERR! node v4.2.3
npm ERR! npm  v2.14.7
npm ERR! code ETIMEDOUT
npm ERR! errno ETIMEDOUT
npm ERR! syscall connect

npm ERR! network connect ETIMEDOUT 151.101.72.162:443
npm ERR! network This is most likely not a problem with npm itself
npm ERR! network and is related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! Please include the following file with any support request:
npm ERR!     H:\blog\npm-debug.log
```

以上错误是因为翻墙安包导致的，在此时你只需要将npm包源指向淘宝即可，即先执行<br/>
```
npm config set registry "https://registry.npm.taobao.org"
```
<br/>
然后再执行 
```
H:\blog>npm install -g hexo-cli 
```
就ok了<br/>
此时在你的C:\User\username\下面有一个后缀为NPMRC的文件，就是你的npm的配置文件，其中内容为registry=https://registry.npm.taobao.org<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在上一步执行完之后，然后执行
```
npm install hexo --save
```
之后执行hexo -v，如果出现以下内容则hexo安装成功<br/>![](http://ox8t0ws1t.bkt.clouddn.com/image/hexo/hexo-v.PNG)<br/>
最后你初始化的时候再你的博客目录下 最好是确认有一个叫hexo的文件夹   确认有了之后再执行 hexo init
<hr/>

以上就是我第二次搭建的时候出现的问题，以及解决方案！