---
layout: post
title: API 设计原则、借鉴和实践
description: API 设计，简单为美！Let Simple Things Simple.
category: blog
---

![](/images/covers/api.jpg)

### 无需怀疑RESTful模式API的普适性

- 坚持使用 API 提供后台服务和数据
- 可以在底层 API 的基础上提供抽象层，方便批量处理请求和返回结果
- 对于常用的包含参数的请求，可提供一个便于记忆的 URL 别名

### 抽象资源，只要一个 endpoint

资源只分两种**实体类**和**动作类**。如：对于一个博客来说，可将用户、文章、类别、评论看作是实
体类资源，而类似于全局搜索文章这样的动作，因一个搜索动作可同时搜索多种资源，可将之归类为动作
类资源。

实体类资源以**实体名称的复数**作为资源名称，如：

    /users              [GET]       # 获取用户列表
    /blogs              [POST]      # 创建一篇文章
    
动作类资源以**动作单词**作为资源名称，如：

    /search?q=design    [GET]       # 获取关键词 design 的搜索结果
    
### 用标准的RESTful请求代替对资源的动作

|HTTP动作                 |对应资源动作                 |
|-------------------------|-----------------------------|
|POST                     |CREATE - 创建                |
|GET                      |READ - 读取、获取数据        |
|PUT                      |UPDATE - 更新                |
|DELETE                   |DELETE - 删除                |

### 对实体资源仅使用两种URL模式

|              |POST           |GET            |PUT            |DELETE           |
|--------------|---------------|---------------|---------------|-----------------|
|/blogs        |创建文章       |查看文章列表   |批量修改       |批量删除         |
|/blogs/1234   |无动作，error  |查看单篇文章   |修改单篇文章   |删除单篇文章     |

### 通过 URL 嵌套来表示资源之间的关系

    /blogs/1234/comments            [GET]       # 获取 ID 为 1234 文章下的评论列表
    /blogs/1234/comments            [POST]      # 为 ID 为 1234 的文章添加一条评论
    /blogs/1234/comments            [DELETE]    # 删除 ID 为 1234 文章下的所有评论
    /users/beetaa/blogs             [GET]       # 获取 ID 为 beetaa 用户的文章列表
    
<div class="message notice">
关联内容的返回方式有两种
<ul>
  <li>返回指向所关联内容的 URL，用户通过点击相关链接再具体查询</li>
  <li>返回具体结果，与主体资源一并返回</li>
</ul>
</div>




[Beetaa]:    http://beetaa.com  "Beetaa"
