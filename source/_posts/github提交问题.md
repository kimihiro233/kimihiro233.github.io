---
title: github提交问题
date: 2024/10/14 17:27:00
categories: [gfw]
tags: [finished]
---

# github提交问题

提交代码时老是提示
``` bash
fatal: unable to access 'https://github.com/kimihiro233/kimihiro233.github.io.git/': Failed to connect to github.com port 443 after 21101 ms
```

目前还没有好的解决办法

尝试切换到ssh拉取的方式，也许可以规避掉无法连接的问题

突然发现通过idea Tools打开会继承代理设置，尝试一下
在ToolBox里设置的代理之后，似乎是稳定了，先观察一段时间，继续解决ssh拉取问题

现在webstorm中无法直接设置ssh配置，找找思路

在.ssh/config中添加配置之后，webstorm就可以正常连接github的ssh服务了
配置如下
```
Host github.com
       HostName github.com
       User git
       IdentityFile ~/.ssh/id_rsa
```