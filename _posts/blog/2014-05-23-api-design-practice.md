---
layout: post
title: API 设计原则、借鉴和实践
description: API 设计，简单为美！Let Simple Things Simple.
category: blog
---

![](/images/covers/api.jpg)

### 鉴定使用RESTful模式API

- 坚持使用 API 提供后台服务和数据
- 可以在底层 API 的基础上提供抽象层，方便批量处理请求和返回结果
- 对于常用的包含参数的请求，可提供一个便于记忆的 URL 别名

### 一个Endpoint一个资源

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

### 只需两种URL模式

|              |POST           |GET            |PUT            |DELETE           |
|--------------|---------------|---------------|---------------|-----------------|
|/blogs        |创建文章       |查看文章列表   |批量修改       |批量删除         |
|/blogs/1234   |无动作，error  |查看单篇文章   |修改单篇文章   |删除单篇文章     |

### 通过URL嵌套实现资源关联

    /blogs/1234/comments            [GET]       # 获取 ID 为 1234 文章下的评论列表
    /blogs/1234/comments            [POST]      # 为 ID 为 1234 的文章添加一条评论
    /blogs/1234/comments            [DELETE]    # 删除 ID 为 1234 文章下的所有评论
    /users/beetaa/blogs             [GET]       # 获取 ID 为 beetaa 用户的文章列表
    
    关联内容的返回方式有两种：
    1、返回指向所关联内容的 URL，用户通过点击相关链接再具体查询；
    2、返回具体结果，与主体资源一并返回。
    可以以 embeded=？？？的方式来指定是否需要将数据嵌入一并返回。

### 将依附于实体资源的操作当成该资源的子集

    /blogs/1234/stars               [GET]       # 获取 ID 为 1234 文章的评星记录
    /blogs/1234/stars               [POST]      # 为文章评星
    /blogs/1234/stars               [DELETE]    # 取消对文章的评星
    
    同样的操作可运用于难度评价、分述评价等动作。
    事实上，这些操作通常是对数据表的一个字段操作，符合子集的定义。

### 将 GET、DELETE 的参数放在 URL 上，用 ？问候一切复杂

- 参数可以包括筛选、排序、分页、查询字段、搜索范围、关键字、删除操作等内容
- 参数串以``?``开头，以``&``分割不同参数，以``=``分割参数和取值，以``,``分
  割多个参数值，以``-``反相
- 参数首单词首字母小写，后面单词首字母大写的方式（与 javascript 保持一致）

<pre><code>/blogs?sort=-priority               [GET]       # 按优先级排序文章
/blogs?stat=open&sort=priority,createdAt&fields=id,name,address
/blogs?q=beetaa                     [GET]       # 以关键字 beetaa 查询文章
</code></pre>

### 将 POST、PUT 的参数放在 JSON 里

- 使用 JSON 传输数据时，记得在请求头加入 ``Content-Type: application/json``

### 限制返回的字段内容

    /blogs?&fields=id,name,address      [GET]

### 返回数据一律采取 JSON 格式

- 对于返回的数据格式有一个统一的包装结构，如层级、内容、名称定义等
- 错误信息亦应使用 JSON 格式返回，并定义良好
- data 是主要数据，是数组，可包含若干数据，每条数据可以嵌套包含关联数据
- page 是分页信息，只返回用于计算结果的基础数据，UI 层可以更加灵活
- error 是错误信息，其中的 url 是解释该错误相信信息的网址

<pre><code>{
  statusCode: 200,
  data: [
    { id: xyz,
      content: blalalala
    }
  ],
  page: {
    pageNumber: 5,
    perPage: 10,
    totalRecord: 158
  },
  error: {
    id: 0x123123123,
    message: yayayaaya,
    description: adfasdfadsfasf,
    url: /adsfadsf/asdfas
  }
}
</code></pre>

### 授权访问

- RESTful API是无状态的也就是说用户请求的鉴权和cookie以及session无关，每一
  次请求都应该包含鉴权证明。
- 认证方法一：SSL。用户可以首先通过一次用户名-密码的验证并得到token，并且可
  以拷贝返回的token到以后的请求中。
- 认证方法二：使用OAuth 2来进行token的安全传输。
- 认证方法三：JSONP 请求无法发送普通的credential。这种情况下可以在查询url中
  添加参数：access_token。

### 其他魔法

- 重要：API 应充分利用 HTTP 自带的缓存机制，如``ETag``、``Last-Modified``等
- 为数据传输开启``gzip``压缩预处理
- 限制查询的速度，预防 DDos 攻击
- 限制查询结果数量，慎防恶意竞争者和数据爬虫
- 始终使用 SSL，安全，且便于认证
- 通过分析``X-HTTP-Method-Override``请求头来实现自定义的请求动作，如``PATCH``等
- API 版本可以使用参数``v``来指定，如``?v=1``、``?v=2``等
- JSON 数据传输前应使用``pretty print``进行美化处理
- 统一提供以纯数字为格式的时间戳，如``1401096133785``，便于 javascript 灵活还原
- 每个资源都有一个唯一的ID，每种资源的ID格式应该是同一的，可使用``UUID``


[Beetaa]:    http://beetaa.com  "Beetaa"
