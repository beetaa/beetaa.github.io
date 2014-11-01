---
layout: post
title: 工作环境配置备忘
description: 基于Win7+Ubuntu@Virtualbox的工作桌面配置过程。
category: blog
---

## 零、总体设想

主操作系统为Win7，用于前端设计和调试。客操作系统为Ubuntu服务器版，用做后端服务器。
两者只能清晰区分：服务器只负责API的运行，客户端则通过IP访问API服务。则开发和调试
过程中，Win7与Ubuntu通过共享文件夹的方式协同，也就是说，所有代码在Win7中编辑，在
Ubuntu中自动检测变动和重启服务器端提供服务。这样做的好处有几个：（1）重分利用Win7
的编辑软件和设计软件运行的流畅性；（2）在开发时就模拟服务器端的环境；（3）做到前
后端开发环境分离，杜绝在一个环境中过于复杂的配置；（4）Virtualbox的便携性。

1. **Win7 核心功能及软件**：
  > - 基本：virtualbox, git, nodejs, npm, vpn, tunnelize, firefox
  > - 编辑器：sublime text 3
  > - 设计：axureRP, photoshop, illustrator
  > - 办公：office2003
  > - node_modules：underscore, 
  > - ionic: jdk, ant, adt,

1. **Ubuntu 核心功能及软件**：
  > - 基本：build-essential
  > - git, nodejs, npm, unrar, unzip

## 一、桌面环境框架

### 1、基础环境

- 主环境：Win7 64位中文版
- 客环境：Docker(Virtualbox+Ubuntu)
- 输入法：搜狗
- 杀毒：百度杀毒
- 浏览器：Firefox + Chrome + IE
- 翻墙：
    > - 基于VPS的VPN全局翻墙
    > - 基于Tunnelize + Foxyproxy(或SwitchyProxy) + SSH的智能代理翻墙

### 2、基础工具

- 办公：
    > - Microsoft Office 2010 64位中文版
    > - Adobe Acrobat 9 Professional 中文版
- 设计：
    > - Adobe Photoshop CS3 中文版
    > - Adobe Illustrator CS3 中文版
    > - AxureRP Professional 7.0
- 编辑器：Sublime Text 3


**附录**

- pageres@[github](https://github.com/sindresorhus/pageres)。
- pageres还可以和[grunt.js](https://github.com/sindresorhus/grunt-pageres)一起使用。
