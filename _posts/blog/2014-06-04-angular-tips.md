---
layout: post
title: AngularJS 实用技术
description: 驾驭AngularJS，驱动下一代前端开发！
category: blog
---

### 一、通过 Service 提供共享数据和功能函数

angularjs最突出的特性之一就是DI，也就是注入，利用factory把需要共享的数据注入
给需要的controller可以干净漂亮的解决这个问题。

    var myApp = angular.module("myApp", []);
     
    myApp.factory('Data', function() {
      return {
        name: "Ting"
      }
    });
     
    myApp.controller('FirstCtrl', function($scope, Data) {
      $scope.data = Data;
     
      $scope.setName = function() {
        Data.name = "Jack";
      }
    });
     
    myApp.controller('SecondCtrl', function($scope, Data) {
      $scope.data = Data;
     
      $scope.setName = function() {
        Data.name = "Moby";
      }
    });
    
参考：[Sharing Data Between Controllers by TIW](https://github.com/tiw/angularjs-tutorial/blob/master/sharing-data-between-controllers.markdown)。以上方法还可以共享公用的功能函数。具体用法可见 [Can I make a function available in every controller in angular?](http://stackoverflow.com/questions/15025979/can-i-make-a-function-available-in-every-controller-in-angular)。

另外，``$rootScope`` 也是共享数据和函数的好地方，而且使用起来更便利。一次定义，全局使用。具体使用上，可在模块的``run``函数中预定义。如：

    <!doctype html>
    <html ng-app="myApp">
    <head>
        <script src="http://code.jquery.com/jquery-1.9.1.min.js"></script>
        <script src="http://code.angularjs.org/1.1.2/angular.min.js"></script>
        <script type="text/javascript">
        var myApp = angular.module('myApp', []);
     
        myApp.run(function($rootScope) {
            $rootScope.globalFoo = function() {
                alert("I'm global foo!");
            };
        });
     
        myApp.controller('MainCtrl', ['$scope', function($scope){
     
        }]);
        </script>
    </head>
    <body ng-controller="MainCtrl">
        <button ng-click="globalFoo()">Call global foo</button>
    </body>
    </html>

### 二、通过 angular-local-storage 实现本地存储

Angular 的本地存储可以直接通过 ``window.LocalStorage`` 进行操作，不过一些库专门做了包装，方便好用。比较看好的是 [ngStorage](https://github.com/gsklee/ngStorage) 和 [angular-local-storage](https://github.com/grevory/angular-local-storage) 两个库。经过比较，最后选择了 angular-local-storage，其实，如果前者的风格更接近 angular，使用也更简单，只是欠缺了一点灵活。

1、安装。从 github 中下载 js 文件包含在自己的 html 页面中即可。

2、将 ``LocalStorageModule`` 作为依赖添加到 **module**，首字母 **大写**

    var myApp = angular.module('myApp', ['LocalStorageModule']);
    
3、通过模块的 **config** 方法进行配置，注意首字母 **小写**

    myApp.config(function (localStorageServiceProvider) {
      localStorageServiceProvider
        .setPrefix('myApp')
        .setStorageType('localStorage')
        .setNotify(true, true)
    });
    
4、通过 **localStorageService** 进行具体使用，首字母 **小写**，值可以是 Json 或 Json 支持的任何格式

    myApp.controller('MainCtrl', function($scope, localStorageService) {
      // 设置键值，返回值是成功与否
      localStorageService.set(key, value);
      // 获取键值
      var value = localStorageService.get(key);
    });

完整的使用方法和API见 [官方文档](https://github.com/grevory/angular-local-storage)。

[Beetaa]:    http://beetaa.com  "Beetaa"
