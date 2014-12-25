---
layout: post
title: Angular + Hapi = RESTful API 的用户认证实战
description: 全面整理基于 Angular 和 Hapi 的 RESTful 应用的用户认证原理、策略和实现。包括 ACL 权限管理。
category: blog
---

使用 Angular 开发基于 RESTful API 的单页应用，不能使用传统的 cookie 和 session 方式。可选的解决方案有 **Token** 、**Oauth** 两种。

## 一、Token 认证
<hr/>

**场景1：**，未登陆的用户在客户端的登陆表单填写邮箱和密码。Angular 调用 ``login()`` 函数将表单信息 **POST** 给服务器 ``/user/login``，服务器检查发来的信息：如果邮箱不存在，返回 **401**；如果邮箱存在但密码不匹配，返回 **401**；如果邮箱和密码均正确，则通过用户信息计算一个唯一的 **Token 字符串** 返回给客户端。客户端解析服务器返回的 **Token**，将其存储在 **SessionStorage** 或 **Local Storage** 中，并将用户状态设置为 **已登陆**。已登陆的用户在后续的每次请求中，事先设置头部信息 ``{"Authorization": Token}``。服务器在收到请求后，校验头部是否存在 Token 信息，以及信息是否准确：没有 Token 或 Token 不准确的，返回 **401**；Token 校验通过但用户权限不够的，返回 **403**；校验通过且具备权限的，返回用户请求的数据。

**什么时候将登陆表单呈现给用户？**1、用户点击 **登陆** 按钮时。2、服务器返回 **401** 时。3、Angular 路由中表明需要登陆才能访问的资源，但 Angular 在客户端检测到用户尚未登陆时。4、程序一开始时（视需求而定）。





## 二、第三方 Oauth 认证
<hr/>

## 三、ACL 权限管理
<hr/>


### 附录1：用户认证好文收录

- [Authentication with AngularJS and a Node.js REST api](http://www.kdelemme.com/2014/03/09/authentication-with-angularjs-and-a-node-js-rest-api/)
- [angular-http-auth](https://github.com/witoldsz/angular-http-auth)
- [ng-token-auth](https://github.com/lynndylanhurley/ng-token-auth#conceptual)
- [Satellizer](https://github.com/sahat/satellizer)