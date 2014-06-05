---
layout: post
title: AngularJS 使用技术
description: 驾驭AngularJS，驱动下一代前端开发！
category: blog
---

### 一、在 Controller 间共享数据

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
    
参考：[Sharing Data Between Controllers by TIW](https://github.com/tiw/angularjs-tutorial/blob/master/sharing-data-between-controllers.markdown)

### 二

[Beetaa]:    http://beetaa.com  "Beetaa"
