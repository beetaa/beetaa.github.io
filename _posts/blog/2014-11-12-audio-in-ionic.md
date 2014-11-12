---
layout: post
title: 在Ionic中播放声音文件
description: 通过 Apache Cordova Media plugin 和 ngCordova 实现
category: blog
---

### 第一步：初始化一个空的工程

    ionic start ionic-project blank
    cd ionic-project
    ionic platform add android
    ionic platform add ios
    # 在非Mac系统中，不能添加 ios
    
### 第二步：安装 Apache Cordova Media plugin

    # 进入项目的根目录
    cordova plugin add org.apache.cordova.media
    
### 第三步：配置 ngCordova

在 [ngCordova](https://github.com/driftyco/ng-cordova/archive/master.zip) 中下载
最新版本的 **ng-cordova.min.js** ，并将其放在 **www/js** 目录下，同时修改 **index.html** 如下：

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">
            <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width">
            <title></title>
            <link href="lib/ionic/css/ionic.css" rel="stylesheet">
            <link href="css/style.css" rel="stylesheet">
            <script src="lib/ionic/js/ionic.bundle.js"></script>
            
            <script src="js/ng-cordova.min.js"></script>
            
            <script src="cordova.js"></script>
            <script src="js/app.js"></script>
        </head>
        <body ng-app="starter">
        
        </body>
    </html>
    
值得注意的是，**ng-cordova.min.js** 需要放在 **cordova.js** 之前，否则将会导致出现错误。

### 第四步：在 app.js 中注入 ngCordova

    angular.module('starter', ['ionic', 'ngCordova']);
    
### 第五步：在 controller 中使用相关功能

    example.controller("ExampleController", function($scope, $cordovaMedia, $ionicLoading) {
     
        # 注册play函数用于播放声音文件
        $scope.play = function(src) {
            var media = new Media(src, null, null, mediaStatusCallback);
            $cordovaMedia.play(media);
        }
     
        # 以下函数被play函数回调，可以很好的根据状态码反馈信息
        # 如果状态码为 Media.MEDIA_STARTING，则显示一个等待图标
        # 否则隐藏等待图标，对于加载互联网音频文件尤其有用，让用户知晓进度
        var mediaStatusCallback = function(status) {
            if(status == 1) {
                $ionicLoading.show({template: 'Loading...'});
            } else {
                $ionicLoading.hide();
            }
        }
     
    });
    
### 第六步：调用play函数播放音频文件

    <ion-content ng-controller="ExampleController">
        <button class="button" ng-click="play('http://www.stephaniequinn.com/Music/Commercial%20DEMO%20-%2013.mp3')">Play from internet</button>
    </ion-content>
    
以上播放的是网上的音频文件，如需播放手机上的本地文件，使用 ``play('www/mp3/song.mp3')`` 来播放位于 
**/storage/emulated/0/www/mp3/song.mp3** 的文件。如需播放服务器的文件，则需要在路径前加上 **/android_asset/** ，
如 ``play('/android_asset/www/mp3/song.mp3')`` 对应的是服务器的 **www/mp3** 目录。

Cordova 还有很多很酷的功能，可参照 ngCordova 或 Apache Cordova Media plugin 的官方文档。


    
原文：[Playing Audio In Your Android And iOS Ionic Framework App](http://blog.nraboy.com/2014/11/playing-audio-android-ios-ionicframework-app/)