---
layout: post
title: Ionic + Angular + Cordova 开发环境配置
description: 完美方案，简单配置。
category: blog
---

### 开发环境摘要

> 操作系统：windows xp 32 bit - 号称 xp 系统的坚守者 ^_^
> JDK：Oracal Java SE Development Kit 7 update 60

### 一、安装 JDK

1. 下载链接：[Oracal Java SE Development Kit 7 update 60](http://download.oracle.com/otn-pub/java/jdk/7u60-b19-demos/jdk-7u60-windows-i586-demos.zip)
2. 安装，路径默认为：``C:\Program Files\Java\jdk1.7.0_60``
3. 配置路径
    
    1. 设置系统变量``JAVA_HOME``为``C:\Program Files\Java\jdk1.7.0_60``
    2. 将 JDK 可执行文件路径``C:\Program Files\Java\jdk1.7.0_60\bin`` 和 JRE 可执行文件路径``C:\Program Files\Java\jre7\bin`` 添加至 Path
4. 测试

### 二、安装 Ant

1. 下载链接：[Apache Ant 1.9.4](http://apache.fayea.com/apache-mirror//ant/binaries/apache-ant-1.9.4-bin.zip)
2. 安装，将 zip 文件直接解压至``C:\Program Files\apache-ant-1.9.4``
3. 配置路径

    1. 设置系统变量``ANT_HOME``为``C:\Program Files\apache-ant-1.9.4``
    2. 将 Ant 可执行文件路径``C:\Program Files\apache-ant-1.9.4\bin`` 添加至 Path
4. 测试

### 三、安装 ADT-Bundle

1. 下载链接：[ADT-Bundle](http://developer.android.com/sdk/index.html)
2. 安装，将 zip 文件直接解压至``C:\Program Files\adt-bundle``
2. 设置系统变量``ANDROID_HOME``为``C:\Program Files\adt-bundle\sdk`` ，**Cordova需要用到这一变量**。
3. 配置路径，将``C:\Program Files\adt-bundle\sdk\platform-tools``和``C:\Program Files\adt-bundle\sdk\tools``加入 Path
4. 为``C:\Program Files\adt-bundle\eclipse\eclipse.exe``建立桌面快捷方式
5. 测试：运行 Eclipse

### 四、配置安卓模拟器

1. ADT-Bundle 的配置程序在``C:\Program Files\adt-bundle\SDK Manager.exe``，可以为其建立桌面快捷方式以便使用
2. 模拟器的配置也在其中进行，``Tools`` -> ``Manage AVDs...`` -> ``New...``

### 五、安装 Cordova + Iconic

    npm install -g cordova gulp iconic      # gulp 是 ionic 的构建工具
    


[Beetaa]:    http://beetaa.com  "Beetaa"
