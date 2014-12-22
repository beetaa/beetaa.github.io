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

    