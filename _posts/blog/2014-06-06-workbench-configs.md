---
layout: post
title: 项目工作环境配置
description: 完美主义者的工作台，需要诸多出乎意料的创新小配置。
category: blog
---

### 一、利用 Dropbox + Git 维护代码仓库

工作原理：
<pre>
+------------+            +-----------+              +---------+
|  Dropbox   |  --Sync->  |  Dropbox  |   --Clone->  | Working |
|   Server   |  <-Sync--  |   Client  |   <-Push---  |  Space  |
+------------+            +-----------+              +---------+
</pre>

实现步骤：

    ~/project $ git init
    ~/project $ git add .
    ~/project $ git commit -m "first commit"
    ~/project $ cd ~/Dropbox/git
    
    ~/Dropbox/git $ git init --bare project.git
    ~/Dropbox/git $ cd ~/project
    
    ~/project $ git remote add origin ~/Dropbox/git/project.git
    ~/project $ git push -u origin master
    
错误解决：

    # 删除 Git 仓库，重建同名的仓库
    $ cd ~/Dropbox/git
    $ rm -rf project.git
    $ git init --bare project.git
    
    # 将保存最新代码的本地仓库 push 回去
    $ git push origin master
    
参考：[Using Git and Dropbox together effectively?](http://stackoverflow.com/questions/1960799/using-git-and-dropbox-together-effectively)

### 二

[Beetaa]:    http://beetaa.com  "Beetaa"
