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

Famo.us 一致在追求 60 FPS 的富内容体验，要达到这个目标，我们需要避免上述的低效率。当我们决定对 DOM 进行抽象时，
我们需要一种可以符合 WEB 开发者对 DOM 的认识预期，又不以牺牲性能为代价的方式。其中，渲染树（Render Tree）是我们
针对**相对定位**和**语义结构**的方案。在另一片文档中，我们将深入讨论事件和动画。

### 创建渲染树

一棵渲染树的起点被称为它的根（ROOT），在传统的 HTML 文档中，``<body>`` 标签就是根。而在 Famo.us 中，根被解释为
上下文（Context）。我们通过 Famo.us 引擎的 ``.createContext`` 方法来实例化一个上下文，这个方法将创建一个带
有 ``famous-container`` CSS 类的 ``<div>`` 标签（也可以通过一个已经存在的 DOM 元素来创建上下文）。

    context                    var context = Engine.createContext();

### 扩展渲染树

上面完成了一个 APP 的创建，但尚没有任何可见的内容，仅仅提供一个 Famo.us 渲染周期的起点。我们可以通过使用 ``.add`` 方
法来为渲染树添加可以显示的节点。平面（Surface）是节点的一种，与 HTML 的 ``<div>`` 标签相对应，这个 ``<div>`` 将
被嵌套在上下文以后的 ``<div>`` 中。结果如下：

    context                    var context = Engine.createContext();
       |
    surface                    context.add(surface);
    
### 节点的种类

一棵渲染树由节点构成。在传统的 HTML 中，这些节点表示为 ``<div>``、``<button>`` 之类的标记。在 Famo.us 中，节点分
为**可渲染（renderables）**和**修改器（modifiers）**。在上面的例子中，我们所添加的平面便是一个可见节点。下面我们
将讨论构成一棵渲染树的典型节点类型。

### 可渲染类节点

可渲染类节点将被绘制在屏幕上。之前的平面节点与 HTML 的 ``<div>`` 标记相关联，其他与 HTML 传统标记对应的节点如下：

|平面节点类型          |对应的 HTML 标记           |
|----------------------|---------------------------|
|Surface               |``<div>``                  |
|ImageSurface          |``<img>``                  |
|InputSurface          |``<input>``                |
|CanvasSurface         |``<canvas>``               |
|VideoSurface          |``<video>``                |

此外还有一种称之为``ContainerSurface``的平面节点，对应在其中嵌套一个 ``Surface`` 节点的 ``<div>`` 标记，常用于设置
了 ``{overflow: hidden} CSS 属性的情况。

所有的平面节点均可自由与任何的 HTML 内容、CSS 样式混用。无论是从一个模板进行渲染还是通过 MVC 绑定数据，Famo.us 对你在平面
中的操作均不会进行干预。但，如果你打算对一系列的 HTML 元素进行独立的动画操作，或通过绑定 DOM 事件监听器来与 APP 的
其他内容进行交互，我们会建议你用一个平面将这些内容包裹起来。平面节点中的内容最好是静态的或者不常变更的。

一个平面节点是 Famo.us 最小的渲染单位，但我们同时支持更加复杂的可见类节点混合，即下面将要讨论的**视图**。

### 修改器节点

修改器是 Famo.us 的另一种节点类型，可用于修改渲染树中该节点所包含的子节点。平面节点很笨，真的！它们不知道自己在页面中
的位置，甚至自己是否可见都不知道。其实这是修改器的工作，修改器对其所包含节点的布局和可视性负责。我们将布局和可视性组
合在一起，是因为在 CSS3 中，变形和透明度是两个依赖于硬件加速的属性，对性能有显著影响。

    context                    var context = Engine.createContext();
       │
    modifier                   var chain = context.add(modifier);
       │
    surface                    chain.add(surface);

上面是一个说明如何对平面节点应用修改器的简化版本。事实上，我们可以通过以下方式来定义一个修改器：

    var modifier = new Modifier({
    
        transform : Transform.translate(100,200)
    });

这样，平面节点将被移动至上下文的 ``top = 100px, left = 200px``，修改器对布局还有很多的强力支持，比如：自动居中、调整
大小等，这些将在另外的教学中讨论。

### 节点的链式修改

修改器根据所在的位置，对渲染树其上的节点产生影响。也就是说，一个修改器可以对另一个修改器产生影响，通过定义一连串的修
改器，这个修改器链条的作用将会被叠加：变形被组合，透明度被累计。这将便于用多个简单的修改器完成复杂的操作，如：一个修
改器负责处理透明度，另一个则专门处理旋转。

    context                    var context = Engine.createContext();
       │
    modifier1                  context.add(modifier1)
       │                             . dd(modifier2)
    modifier2                         .add(surface);
       │
    surface
    
### 节点分支

到目前为止，我们的渲染树还是一根筋：一个节点紧接另一个节点。事实上，节点分支才是渲染树有趣的部分。下面的例子描述了如
何通过在同一节点下连续使用 ``.add`` 方法来产生分支：

          context                var context = Engine.createContext();
       ┌─────┴─────┐
    modifier    surface2         context.add(modifier).add(surface1); // 左边分支
       │
    surface1                     context.add(surface2);               // 右边分支

节点分支是对可渲染节点进行相对定位的关键，如：

          context                var context = Engine.createContext();
             │
         modifier1               var relativeNode = context.add(modifier1);
       ┌─────┴─────┐
    modifier2   surface2         relativeNode.add(modifier2).add(surface1);
       │
    surface1                     relativeNode.add(surface2);

在上面的例子中，surface1 和 surface2 同时相对 modifier1 进行相对定位，其中，surface1 在此基础上叠加应用了 modifier2 的
定位数据（假设这些修改器仅用于定位修改）。

### 视图

到目前为止，我们已经了解如何在渲染树中添加修改器和平面节点。你可以想象一下如何通过乐高积木创建更加复杂的组件。为了减
少开发者创建组件的重复工作，Famo.us 提供 ``View`` 视图基类，该类提供向渲染树添加内容（包括可渲染节点和修改器节点）、
接收和广播事件、接收缺省参数、定义变量等的接口。同时，Famo.us 框架自身已包括一个通用的视图库（期待社区为此添砖加瓦）。
我们将在其他文档中讨论视图如何处理事件和变量声明。在这里，我们只讨论如何通过视图来扩展渲染树，以及维护视图中的内部
渲染树（子树）。

在下面的例子中，我们添加了一个 ``Scrollview`` ：

    context                var context = Engine.createContext()
       │
    modifier               context.add(modifier).add(scrollview);
       │
    scrollview

从内部看，``Scrollview`` 有着自己复杂的内部逻辑，但开发者只需简单地如其他节点一样将至添加到渲染树中，而无需关注其内部
逻辑。这是 Famo.us 对 Shadow DOM 的实现。``Scrollview`` 初始化后，我们就可以通过它的 ``sequenceFrom`` 接口填充可渲染
节点，这些节点将被创建为 ``Scrollview`` 组件的内部渲染树。

         scrollview              scrollview.sequenceFrom([S1, S2, S3, ... , S10]);
     ┌───┬───┼───────┐
     S1  S2  S3  ⋯  S10

需要注意的是，上面例子中的 ``S10`` 并不一定是 Famo.us 的平面节点，它可以是另一个包含自身修改器和其他节点的视图，甚至
可以是另外一个 ``Scrollview``（也就是说，视图可以嵌套 --译者注）。如果 ``S10`` 是另一个视图且结构如下，你可以设置
``Scrollview`` 第一个元素的透明叠加属性（Cross-fading Opacity）。

             S10                 S10.add(modifier1).add(surface1);
        ┌─────┴─────┐
    modifier1   modifier2        S10.add(modifier2).add(surface2);
        │           │
    surface1    surface2

这时的渲染树结构将如下：

          context
             │
          modifier
             │
         scrollview
     ┌───┬───┼───────┐
    S1  S2  S3  ⋯  S10
               ┌─────┴─────┐
           modifier1    modifier2
               │           │
           surface1     surface2

通过视图对复杂的逻辑进行包装，我们可以更好地管理 APP。相比于 DOM，不会因为结构嵌套而导致性能受损，渲染树中的所有东西
在转换为 DOM 的时候都是扁平结构的。

### 简要概括

> 修改器就是一切。 -- Anon

在上面所有的范例中，你会注意到一个模式：一棵渲染树始于一个上下文，经由包含一系列修改器的分支发散开，并以一个平面结尾。
DOM 将可视元素和语义表达混合在一起，而渲染树则将之明确区分为布局（通过修改器节点）、内容（通过平面节点）和结构（通过
 ``.add`` 方法）。
 
事实上，如果你需要知道渲染树某个平面节点的位置、透明度，只需计算其上修改器的透明度和变形数据即可。

两者的另一个不同点在于，DOM 在节点样式或内容发生变化后都需要重绘（即时模式），而 Famo.us 则是在后台通过 ``requestAnimationFrame`` 
对需要处理的变更进行缓冲和批量处理（保留模式）。这些变更将被适时处理（与显示器刷新率同步）。

总的来说，Famo.us 的渲染树和传统的 DOM 比较如下：

|                       |Famo.us 渲染树             |DOM                       |
|-----------------------|---------------------------|--------------------------|
|树形结构               |是                         |是                        |
|节点                   |可渲染节点 + 修改器节点    |HTML 元素                 |
|需要重新梳理           |否                         |是                        |
|包装                   |视图 + 组件                |Shadow DOM                |
|含义                   |结构                       |结构 + 渲染               |
|渲染周期               |保留模式                   |即时模式                  |
|语言                   |Javascript                 |HTML                      |


---

[本文](http://beetaa.com/the-famo-us-render-tree/)为[个人](http://beetaa.com/)原创
翻译[作品](http://famo.us/guides/dev/render-tree.html)，可随意转载，但期待能保留原文链接。十分感谢。

