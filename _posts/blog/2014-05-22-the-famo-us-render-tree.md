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

Famo.us 一致在追求 60 FPS 的富内容体验，要达到这个目标，我们需要避免上述的低效率。当我们决定对 DOM 进行抽象时，我们需要一种
可以符合 WEB 开发者对 DOM 的认识预期，又不以牺牲性能为代价的方式。其中，渲染树（Render Tree）是我们针对**相对定位**和**语义
结构**的方案。在另一片文档中，我们将输入讨论事件和动画。

### 创建渲染树

一棵渲染树的起点被称为它的根（ROOT），在传统的 HTML 文档中，``<body>`` 标签就是根。而在 Famo.us 中，根被解释为上下文（Context）。
我们通过 Famo.us 引擎的 ``.createContext`` 方法来实例化一个上下文，这个方法将创建一个带有 ``famous-container`` CSS 类的 ``<div>`` 
标签（也可以通过一个已经存在的 DOM 元素来创建上下文）。

    context                    var context = Engine.createContext();

### 扩展渲染树

上面完成了一个 APP 的创建，但尚没有任何可见的内容，仅仅提供一个 Famo.us 渲染周期的起点。我们可以通过使用 ``.add`` 方法来为
渲染树添加可以显示的节点。平面（Surface）是节点的一种，与 HTML 的 ``<div>`` 标签相对应，这个 ``<div>`` 将被嵌套在上下文以后
的 ``<div>`` 中。结果如下：

    context                    var context = Engine.createContext();
       |
    surface                    context.add(surface);
    
### 节点的种类

一棵渲染树由节点构成。在传统的 HTML 中，这些节点表示为 ``<div>``、``<button>`` 之类的标记。在 Famo.us 中，节点分
为**可见类（renderables）**和**调整类（modifiers）**。在上面的例子中，我们所添加的平面便是一个可见节点。下面我们
将讨论构成一棵渲染树的典型节点类型。

### 可见类节点

可见类节点将被绘制在屏幕上。之前的平面节点与 HTML 的 ``<div>`` 标记相关联，其他与 HTML 传统标记对应的节点如下：

|平面节点类型          |对应的 HTML 标记           |
|----------------------|:-------------------------:|
|Surface               |``<div>``                  |
|ImageSurface          |``<img>``                  |
|InputSurface          |``<input>``                |
|CanvasSurface         |``<canvas>``               |
|VideoSurface          |``<video>``                |

此外还有一种称之为``ContainerSurface``的平面节点，对应在其中嵌套一个 ``Surface`` 节点的 ``<div>`` 标记，常用于设置
了 ``{overflow: hidden} CSS 属性的情况。
