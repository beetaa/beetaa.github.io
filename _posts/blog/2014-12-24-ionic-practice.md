---
layout: post
title: Ionic 移动框架开发实践
description: 基于 Angular.js 的一个移动开发框架。
category: blog
---

### Ionic 路由模块使用的是 ``ui-router``，而非 ``ngRoute``

因此，在 Controller 中应该使用 ``$stateParams`` 来获得 ``url`` 的参数，而非 ``$routeParams``。**ui-router** 是对 Angular.js 自带路由模块 **ngRoute** 的增强，使用方法详见 [ui-router 官方文档](https://github.com/angular-ui/ui-router/wiki/URL-Routing#stateparams-service)。



