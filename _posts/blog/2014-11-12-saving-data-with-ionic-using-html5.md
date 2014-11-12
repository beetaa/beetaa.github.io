---
layout: post
title: 在Ionic中存储数据-HTML5模式
description: 使用内置的html5存储功能在ionic中存储数据
category: blog
---

### HTML5 Local Storage API 的一般使用方法

    if(typeof(Storage) != "undefined") {
        localStorage.setItem("firstname", "Nic");
        localStorage.setItem("lastname", "Raboy");
        alert(localStorage.getItem("firstname") + " " + localStorage.getItem("lastname"));
    } else {
        alert("Sorry, your browser does not support Web Storage...");
    }

从以上例子可以看出，可以通过 ``setItem`` ``getItem`` ``removeItem`` 来管理本地数据。
这三个函数在 **ionic** 中同样适用。

### 在 ionic 中使用 local storage api

    myApp.controller('Login', function($scope) {
        $scope.login = function(username, password) {
            window.localStorage.setItem("username", username);
            window.localStorage.setItem("password", password);
        };
     
        $scope.isLoggedIn = function() {
            if(window.localStorage.getItem("username") !== undefined && window.localStorage.getItem("password") !== undefined) {
                return true;
            } else {
                return false;
            }
        };
     
        $scope.logout = function() {
            window.localStorage.removeItem("username");
            window.localStorage.removeItem("password");
        };
    });

### 使用 JSON.stringify 和 JSON.parse 来处理复杂数据

    myApp.controller('Profile', function($scope, $http) {
        $http.get("https://api.example.com/profile", { params: { "api_key": "some_key_here" } })
            .success(function(data) {
                $scope.profile = data;
                window.localStorage.setItem("profile", JSON.stringify(data));
            })
            .error(function(data) {
                if(window.localStorage.getItem("profile") !== undefined) {
                    $scope.profile = JSON.parse(window.localStorage.getItem("profile"));
                }
            });
    });
    
    
    
原文：[Saving Data With IonicFramework](http://blog.nraboy.com/2014/06/saving-data-with-ionicframework/)