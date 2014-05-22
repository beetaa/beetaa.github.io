---
layout: post
title: Famo.us 渲染树 - 翻译
description: 介绍 Famo.us 框架渲染基础技术，翻译自官网 [The Famo.us Render Tree](http://famo.us/guides/dev/render-tree.html) 。
category: blog
---

开发者首先要关注的事情是： Famo.us 将尽可能少地暴露 HTML 和 DOM 。DOM 交互有性能和理解的问题。 Famo.us 通过在 Javascript 中
将 DOM 操作抽象为一棵渲染树（Render Tree）来进行管理。

如果你在观察一个使用 Famo.us 框架的网站， 你会发现 DOM 结构是非常扁平化的：绝大多数元素是作为另一元素的同层级。而在观察其他
网站时，DOM 的结构却是重度嵌套的。
