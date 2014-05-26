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
- 对于诸如加星|取消加星|评分|取消评分等依附于实体资源的操作，可将其视为

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
    
    关联内容的返回方式有两种：
    1、返回指向所关联内容的 URL，用户通过点击相关链接再具体查询；
    2、返回具体结果，与主体资源一并返回。

### 将依附于实体资源的操作当成该资源的子集

    /blogs/1234/stars               [GET]       # 获取 ID 为 1234 文章的评星记录
    /blogs/1234/stars               [POST]      # 为文章评星
    /blogs/1234/stars               [DELETE]    # 取消对文章的评星
    
    同样的操作可运用于难度评价、分述评价等动作。

### 用参数扩展 GET、DELETE 操作，用 ？问候一切复杂

- 参数可以包括筛选、排序、分页、查询字段、搜索范围、关键字、删除操作等内容
- 参数串以``?``开头，以``&``分割不同参数，以``=``分割参数和取值，以``,``分割多个参
  数值，以``-``反相

<pre><code>
/blogs?sort=-priority               [GET]       # 按优先级排序文章
/blogs?stat=open&sort=priority,created_at&fields=id,name,address
/blogs?q=beetaa                     [GET]       # 以关键字 beetaa 查询文章
</code></pre>

### 限制返回的字段内容

    /blogs?&fields=id,name,address      [GET]
    
### 其他魔法


[Beetaa]:    http://beetaa.com  "Beetaa"
