---
layout: post
title: 项目工作环境配置
description: 完美主义者的工作台，需要诸多出乎意料的创新小配置。
category: blog
---

### 一、利用 Dropbox + Git 维护代码仓库

1、实现原理：

    +------------+            +-----------+              +---------+
    |  Dropbox   |  --Sync->  |  Dropbox  |   --Clone->  | Working |
    |   Server   |  <-Sync--  |   Client  |   <-Push---  |  Space  |
    +------------+            +-----------+              +---------+

2、实现步骤：

    # 初始化本地代码库
    ~/project $ git init
    ~/project $ git add .
    ~/project $ git commit -m "first commit"
    
    # 在 Dropbox 中创建 Git 仓库
    ~/project $ cd ~/Dropbox/git
    ~/Dropbox/git $ git init --bare project.git
    
    # 将本地仓库关联并推送至 Dropbox 仓库
    ~/Dropbox/git $ cd ~/project
    ~/project $ git remote add origin ~/Dropbox/git/project.git
    ~/project $ git push -u origin master
    
3、错误解决：

    # 删除 Git 仓库，重建同名的仓库
    $ cd ~/Dropbox/git
    $ rm -rf project.git
    $ git init --bare project.git
    
    # 将保存最新代码的本地仓库 push 回去
    $ git push origin master
    
4、参考文档：
> [Using Git and Dropbox together effectively?](http://stackoverflow.com/questions/1960799/using-git-and-dropbox-together-effectively)
> [Using Dropbox as a Private GitHub](http://jetheis.com/blog/2013/02/17/using-dropbox-as-a-private-github/)

### 二

[Beetaa]:    http://beetaa.com  "Beetaa"
