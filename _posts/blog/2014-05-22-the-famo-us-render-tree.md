---
layout: post
title: Famo.us 渲染树 - 翻译
description: 介绍 Famo.us 框架渲染基础技术，翻译自官网 [The Famo.us Render Tree](http://famo.us/guides/dev/render-tree.html) 。
category: blog
---

开发者首先要关注的事情是： Famo.us 将尽可能少地暴露 HTML 和 DOM 。DOM 交互有性能和理解的问题。 Famo.us 通过在 Javascript 中
将 DOM 操作抽象为一棵渲染树（Render Tree）来进行管理。

如果你在观察一个使用 Famo.us 框架的网站， 你会发现 DOM 结构是非常扁平化的：绝大多数元素是作为另一元素的同层级。而在观察其他
网站时，DOM 的结构却是重度嵌套的。在对待 HTML 的问题上，Famo.us 与传统网站有着本质的区别：我们将 HTML 页面的结构保存于 
Javascript 中，对我们来说，HTML 的元素并非你所看到的整个页面的真实结构，而是一系列需要在屏幕上绘制的元素清单。

开发者习惯于嵌套使用 HTML 元素，因为这便于元素的**相对定位**、**事件冒泡**和实现**语义结构**。然而，实现这些目标都需要付出
成本，如：相对定位会导致页面在重排动画内容的时候变慢；在没有妥善管理时间传播时，事件冒泡成本高昂；同时，页面的语义结构也不
利于很好地分离 HTML 和视图渲染。


