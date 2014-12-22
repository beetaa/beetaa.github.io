---
layout: post
title: hapijs API 开发实践
description: 基于 nodejs 的一个 API 开发框架。
category: blog
---

### 一、安装

    npm install hapi --save
    
### 二、完整范例

    var Hapi = require('hapi');
    
    // 创建服务器
    
    var server = new Hapi.Server();
    server.connection({ port: 3000 });
    
    // 配置API路由
    
    server.route({
        method: 'GET',
        path: '/',
        handler: function (request, reply) {
            reply('Hello, world!');
        }
    });
    
    server.route({
        method: 'GET',
        path: '/{name}',
        handler: function (request, reply) {
            reply('Hello, ' + encodeURIComponent(request.params.name) + '!');
        }
    });
    
    // 启动服务器
    
    server.start(function () {
        console.log('API 服务器运行在:', server.info.uri);
    });

### 使用插件

1、首先要安装相关的插件，如：

    npm install good --save
    npm install good-console --save
    
``good`` 是一个访问日志插件，``good-console`` 是 ``good`` 插件的报告功能模块。

2、通过 register 函数注册并使用插件

    var Hapi = require('hapi');
    
    // 引入插件
    
    var Good = require('good');
    
    var server = new Hapi.Server();
    server.connection({ port: 3000 });
    
    server.route({
        method: 'GET',
        path: '/',
        handler: function (request, reply) {
            reply('Hello, world!');
        }
    });
    
    server.route({
        method: 'GET',
        path: '/{name}',
        handler: function (request, reply) {
            reply('Hello, ' + encodeURIComponent(request.params.name) + '!');
        }
    });
    
    // 注册使用插件
    
    server.register({
        register: Good,
        options: {
            reporters: [{
                reporter: require('good-console'),
                args:[{ log: '*', response: '*' }]
            }]
        }
    }, function (err) {
        if (err) {
            throw err; // 如果插件加载过程中出现错误
        }
    
        server.start(function () {
            server.log('info', 'API 服务器运行在: ' + server.info.uri);
        });
    });

    