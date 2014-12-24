---
layout: post
title: AngularJS 实用技术
description: 驾驭AngularJS，驱动下一代前端开发！
category: blog
---

### 一、通过 Service 提供共享数据和功能函数

angularjs最突出的特殊之一就是DI，也就是注入，利用factory把需要共享的数据注入
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

### 二

[Beetaa]:    http://beetaa.com  "Beetaa"
