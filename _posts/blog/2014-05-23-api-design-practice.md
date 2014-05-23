---
layout: post
title: API 设计原则、借鉴和实践
description: API 设计，简单为美！Let Simple Things Simple.
category: blog
---

![](/images/covers/api.jpg)

### 抽象资源

资源只分两种：**实体类** 和 **动作类**。如：对于一个博客来说，可将用户、文章、类别、评论看作是
实体类资源，而类似于全局搜索文章这样的动作，因一个搜索动作可同时搜索多种资源，可将之归类为动作
类资源。

#### 实体类资源以 **实体名称的复数** 作为资源名称，如：

- 用户：``Get /users``
- 文章：``Post /users``

#### 动作类资源以 **动作单词** 作为资源名称

- 搜索：``Get /search?q=design``



[Beetaa]:    http://beetaa.com  "Beetaa"
