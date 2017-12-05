---
title: 错误共享
date: 2017-09-28 18:16:05
tags: [github, hexo, Error]
categories: ERROR
copyright: true
---
<h2>部署时出现的错误</h2>
>今天在优化完主题，部署的时候不知道为什么突然间出现了无法连接到远程仓库的错误，如下所示
```
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: Authentication failed.
fatal: Could not read from remote repository.
Please make sure you have the correct access rights
and the repository exists.
```
<!--more-->
于是在伟大的firefox查询了好久，但还是没有具体弄明白究竟是怎么回事，于是我就在git上重新生成密钥，语法如下：

```
$ ssh-keygen -t rsa -C "574844241@qq.com"
```

>然后在[github](https://github.com/settings/keys)上又new SSH KEY ，将C:/用户/user/id_rsa.pub中的内容添加在new出来的key中了；然后通过以下语法测试

```
ssh -T git@github.com
```
>出现"Hi wangshiyibazhang! You've successfully authenticated, but GitHub does not provide shell access."的提示就ok了！

不过我今天将域名已经配置好了，嘻嘻。。。