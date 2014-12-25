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

    server.route({
        method: 'GET',
        path: '/hello/{user}',
        handler: function(request, reply) {},
        config: {}
    });

1、**method** 取值可以是任何有效的 ``http`` 请求方法，可通过字符串或数组来指定，如 ``'GET'``, ``'POST'``, ``['PUT', 'POST']`` 等。

2、**path** 可指定命名参数，如``'/hello/{user}'``。路径的每一个分段只能有一个命名参数。如：``/{filename}.jpg`` 是正确的，``/{filename}.{ext}`` 则是非法的。

3、在指定命名参数的时候，可将该参数定义为可选的、非必要的，如 ``/hello/{user?}``，这时，通过 ``/hello/susan`` 和 ``/hello`` 的形式均可访问。但要注意的是：**只有最后一个参数可设为可选**，如 ``/{one?}/{two}`` 这样的模式是不被接受的。

4、多分段参数。在命名参数后面加上一个 ``*`` 号，则代表这个参数是多分段参数。如 ``/hello/{user*}``，通过 ``/hello/zhao/yi/ya`` 的形式访问时，``request.params.user`` 的值将是字符串 ``'zhao/yi/ya'``，可通过字符串的 ``split('/')`` 方法转换为一个数组进行处理。注意，和可选参数一样：**只有最后一个参数可设为多分段参数**。

3、命名参数存储在``request.params``对象中，可通过``request.params.user``访问。而通过在地址栏中以``?key=value``形式指定的请求参数，可通过``request.query.key``访问。

4、为防止内容注入攻击，可通过``encodeURIComponent(request.params.user)``对内容编码净化，但通过编码的中文和其他非标准字符将会是``%E8%B5%B5``的形式。

5、**handler** 函数的 request 包含来自用户端的详细请求信息，如路径参数、附带的正文数据(payload)、认证信息、请求头部信息等。handler 函数的 reply 用来反馈信息，反馈的内容可以是文本、buffer、Json对象、读写流。reply 方法返回一个 response 对象，我们可对其进行链式调用，如设置头信息、``content type``、重定向等。

6、**config** 选项是可选的，可对每一个路由进行单独的设置，如：数据校验、身份验证、前置处理、附加数据处理、缓存选项等。

### 三、通用方法 - Server Methods

通用方法可让你在整个服务器范围内共享那些通用的功能。可通过以下两种方法注册通用方法。函数可以有任意数量的参数，但最后一个参数必须是 ``next()``，这是函数的回调，用于处理返回结果。回调函数的格式为 ``callback(err, result, ttl)``，如果在函数处理过程中发生错误，可通过 ``next(err)`` 的形式返回；如没有发生错误，可通过 ``next(null, result)`` 的形式返回。

方法1，一次注册一个函数：

    var add = function(x, y, next) {
        next(null, x + y);
    };
     
    server.method('add', add, {});
    
方法2，一次可以注册一个或多个函数：

    var add = function(x, y, next) {
        next(null, x + y);
    };
     
    var multi = function(x, y, next) {
        next(null, x * y);
    };
     
    server.method([
        {name: 'add', method: add, options: {}},
        {name: 'multi', method: multi, options: {}}
    ]);
    
通用方法的执行结果可以缓存，还有更多特性，详见 [官方文档](http://hapijs.com/tutorials/server-methods)。

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

    var server = new Hapi.Server({
        host: '0.0.0.0',
        port: 8080,
        routes: {
            cors: true
        }
    );

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