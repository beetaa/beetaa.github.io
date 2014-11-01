---
layout: post
title: 工作环境配置备忘
description: 基于Win7+Ubuntu@Virtualbox的工作桌面配置过程。
category: blog
---

主操作系统为Win7，用于前端设计和调试。客操作系统为Ubuntu服务器版，用做后端服务器。
两者只能清晰区分：服务器只负责API的运行，客户端则通过IP访问API服务。则开发和调试
过程中，Win7与Ubuntu通过共享文件夹的方式协同，也就是说，所有代码在Win7中编辑，在
Ubuntu中自动检测变动和重启服务器端提供服务。这样做的好处有几个：（1）重分利用Win7
的编辑软件和设计软件运行的流畅性；（2）在开发时就模拟服务器端的环境；（3）做到前
后端开发环境分离，杜绝在一个环境中过于复杂的配置；（4）Virtualbox的便携性，并享受
Win7主系统的翻墙设置。

**Win7 核心功能及软件：**

- 基本：virtualbox, git, nodejs, npm, vpn, tunnelize, firefox
- 编辑器：sublime_text 3
- 设计：axureRP, photoshop, illustrator
- 办公：office2003, acrobat
- node_modules：bower, gulp, cordova, ionic, live-server
- ionic环境: jdk, ant, adt
- 其他：winrar, 迅雷, python, youtube_dl

**Ubuntu 核心功能及软件：**

- 基本：build-essential, virtualbox_addons, git, unrar, unzip
- 基本：nodejs, npm, redis, mongodb, nginx
- node_modules：underscore, redis, mongoose, gulp, express, sock.io, hapi, nodemon
- 其他：配置与win7共享目录


## 一、Win7环境配置

**VPN全局翻墙**

1. 在VPS服务器中[安装及配置VPN服务](http://#)
2. 在Win7中新建VPN链接，如下图

**Tunnelize局部翻墙**

1. 在openshift中新建一个app，得到ssh访问url
2. 本地生成公私秘钥对，将公钥上传至openshift
3. 安装配置tunnelize，并让其开机自动运行
4. 配置firefox + foxyproxy


**附录**

- pageres@[github](https://github.com/sindresorhus/pageres)。
- pageres还可以和[grunt.js](https://github.com/sindresorhus/grunt-pageres)一起使用。
