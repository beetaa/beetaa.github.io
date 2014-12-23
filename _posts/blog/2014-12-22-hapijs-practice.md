---
layout: post
title: hapijs API 开发实践
description: 基于 nodejs 的一个 API 开发框架。
category: blog
---

### 一、安装

1、安装 hapijs

    npm install hapi --save
    
2、安装 hapijs 插件

    npm install good
    npm install good-console
    
``good`` 是一个访问日志插件，``good-console`` 是 ``good`` 插件的报告功能模块。官方网站有[完整的插件列表](http://hapijs.com/plugins)。
    
### 二、完整范例

    // 引入 hapijs
     
    var Hapi = require('hapi');
     
    // 引入插件
     
    var Good = require('good');
     
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
        }
    );
     
    // 启动服务器
     
    server.start(function () {
        console.log('API 服务器运行在:', server.info.uri);
    });

### 三、路由 - Routes

**method**: 取值可以是任何有效的``http``请求方法，可通过字符串或数组来指定，如``'GET'``, ``'POST'``, ``['PUT', 'POST']``等。

**path**: 1、可指定命名参数，如``'/hello/{user}'``，这个名为``user``的参数存储在``request.params``对象中，可通过``request.params.user``访问。2、为防止内容注入攻击，可通过``encodeURIComponent(request.params.user)``对内容编码净化。

### 附录1：解决 Angular + Hapi 的跨域访问问题

1、服务器端，在``reply``的``header``中加入相关头信息，明确指出服务器可接受跨域访问。

    server.route({
        handler: function(request, reply) {
            reply('something')
                .header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept')
                .header('Access-Control-Allow-Origin', '*');
            }
        }
    );
    
或者使用``server.route()``选项的``config.cors``属性。

    server.route({
        handler: function(request, reply) {
            reply('something');
        },
        config: {
            cors: {origin: '*'}
        }
    });
    
``cors``属性值可以是``true``，也可以是一个包含``origin``、``matchOrigin``等属性的对象。详情见[官方文档关于cors的说明](http://hapijs.com/api#route-options) 。
    
另外，hapijs 还允许对 ``cors`` 进行全局设定，具体是在``new Hapi.server()``中指定``cors``配置：

    var server = new Hapi.Server(host,port,{ cors: true });

2、Angular 端，需要在 module.config 中设置 $http 服务。

    app.config(['$httpProvider', function($httpProvider) {
        $httpProvider.defaults.useXDomain = true;
        // 如果服务器已经设置 Access-Control-Allow-Origin: "*",
        // $httpProvider.defaults.withCredentials = true;
        delete $httpProvider.defaults.headers.common["X-Requested-With"];
        $httpProvider.defaults.headers.common["Accept"] = "application/json";
        $httpProvider.defaults.headers.common["Content-Type"] = "application/json";
    }]);
    
注意：Angular 中的 ``$httpProvider.defaults.withCredentials = true`` 与 服务器端的 ``Access-Control-Allow-Origin: "*"`` 不能同时设置，所以在这里要注释掉。

关于 $http 服务还有两个需要注意的地方：一，以上设置可以在每一次请求前通过``$http(options)``进行覆盖；二、官方文档中提到``csrf``的问题有与Cookie相关的操作，不知是否对跨域访问有影响？参考文档：[Agularjs 官方 API 说明](https://docs.angularjs.org/api/ng/service/$http) 和 [Stackoverflow 相关问题的解答](http://stackoverflow.com/questions/17289195/angularjs-post-data-to-external-rest-api)。