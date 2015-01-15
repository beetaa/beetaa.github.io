---
layout: post
title: Angular + Hapi = RESTful API 的用户认证实战
description: 全面整理基于 Angular 和 Hapi 的 RESTful 应用的用户认证原理、策略和实现。包括 ACL 权限管理。
category: blog
---

使用 Angular 开发基于 RESTful API 的单页应用，不能使用传统的 cookie 和 session 方式。可选的解决方案有 **Token** 、**Oauth** 两种。

## 一、Token 认证
<hr/>

**场景：**，未登陆的用户在客户端的登陆表单填写邮箱和密码。Angular 调用 ``login()`` 函数将表单信息 **POST** 给服务器 ``/user/login``，服务器检查发来的信息：如果邮箱不存在，返回 **401**；如果邮箱存在但密码不匹配，返回 **401**；如果邮箱和密码均正确，则通过用户信息计算一个唯一的 **Token 字符串** 返回给客户端。客户端解析服务器返回的 **Token**，将其存储在 **SessionStorage** 或 **Local Storage** 中，并将用户状态设置为 **已登陆**。已登陆的用户在后续的每次请求中，事先设置头部信息 ``{"Authorization": Token}``。服务器在收到请求后，校验头部是否存在 Token 信息，以及信息是否准确：没有 Token 或 Token 不准确的，返回 **401**；Token 校验通过但用户权限不够的，返回 **403**；校验通过且具备权限的，返回用户请求的数据。

**什么时候将登陆表单呈现给用户？**1、用户点击 **登陆** 按钮时。2、服务器返回 **401** 时。3、Angular 路由中表明需要登陆才能访问的资源，但 Angular 在客户端检测到用户尚未登陆时。4、程序一开始时（视需求而定）。

Token 其实只是一个经加密以后的字符串。有多种生成、管理机制可供选择，如 **hawk** 、**jwt**、**signature** 等，在官方网站的插件栏都有相关的插件。我们也可以自定义自己的字符串和验证机制，如：计算一个加密的字符串，并且将这个字符串当做一个签名字段保存在用户数据库或缓存中，检查每次用户端发来的 header，反查签名即可得到用户信息。我选用的是最常用的 **jwt** 机制，相关的插件是 [hapi-auth-jwt](https://github.com/ryanfitz/hapi-auth-jwt)。**jwt** 是 [Json Web Token](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) 的简称，它 的处理流程是：在服务器端，通常是处理用户登陆的流程中，给出一个 json 数据（通常是用户的相关信息，如用户id、email等有唯一性的数据）和一个私密的 key，调用 ``jwt.sign(json, key)`` 即可生成一个 Token 字符串。成功登陆以后，服务器将 Token 通过 ``Bearer <Token 字符串>`` 的格式返回客户端。客户端在以后的每一次请求中，将头部的 **Authorization** 字段设置为该内容。服务器在收到请求后，通过``jwt.verify(token, key, function(err, decodedJson) {})`` 方法 **对 Token 信息进行解码，得到加密之前的 json 对象**，这个对象中包含 **用户id** 或 **email** 等用户唯一数据，系统据此在用户数据库查找相关记录，能找到，则表示验证通过，找不到，则拒绝该请求。这个处理的具体过程可参考 [http-auth-jwt 源代码](https://github.com/ryanfitz/hapi-auth-jwt/blob/master/lib/index.js)。





## 二、第三方 Oauth 认证
<hr/>

## 三、ACL 权限管理
<hr/>


### 附录1：用户认证好文收录

- [Authentication with AngularJS and a Node.js REST api](http://www.kdelemme.com/2014/03/09/authentication-with-angularjs-and-a-node-js-rest-api/)
- [angular-http-auth](https://github.com/witoldsz/angular-http-auth)
- [ng-token-auth](https://github.com/lynndylanhurley/ng-token-auth#conceptual)
- [Satellizer](https://github.com/sahat/satellizer)
- [hapi-auth-jwt](https://github.com/ryanfitz/hapi-auth-jwt)