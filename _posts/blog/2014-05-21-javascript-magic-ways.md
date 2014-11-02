---
layout: post
title: Javascript & nodejs 技巧小集
description: 一些 JS 编程小技巧、小片段，不惊世，不骇俗，关键要实用
category: blog
---

### nodejs原生事件编程模式 - util.inherits方式

    # 事件编程以来的两个库events, util
    var events = require('events');
    var util = require('util');
     
    # 定义需要事件化的类，并使用util.inherits工具让其继承event.EventEmitter
    var MyClass = function() {
        events.EventEmitter.call(this);
    }
    util.inherits(MyClass, events.EventEmitter);
     
    # 通过自定义类的prototype来定义具体的方法，一般在其中Emit出事件
    MyClass.prototype.myfun_01 = function(data) {
        # 注册event_01事件，并将data作为附带的参数进行传递
        this.emit('event_01', data);
        # 返回类的实例，方便链式调用
        return this;
    }
     
    # 将类实例化
    var myclass_01 = new MyClass();
    # 注册该实例的事件器
    myclass_01.on('event_01', function(data) {
        console.log('侦听到事件event_01, 其传递的参数为：' + data);
    });
     
    # 在适当的时候调用该实例的myfun_01方法，即可触发event_01事件
    myclass_01.myfun_01('我是myfun_01方法，调用后触发event_01事件，这条消息就是事件附带的参数');
    
    
### nodejs原生事件编程模式 - __proto__方式

    var EventEmitter = require('events').EventEmitter;
     
    var MyClass = function() {
        //这里以this方式定义数据和方法
    }
     
    MyClass.prototype.__proto__ = EventEmitter.prototype;
     
    # 以下就一样了
    
    
### nodejs包的编写规范和使用

    #如果包需要用到事件，则引入events模块
    var EventEmitter = require('events').EventEmitter;
     
    # 通过包的名称直接可以引用一个初始化的实例
    # 如：var pack = require('./my_packaage')
    # pack 变量直接就是一个实例化以后的包
    exports = module.exports = new Package();
     
    # 通过在包名称后面引用暴露后的名字，可以得到未初始化的类
    # 这样可以在使用时通过 new 关键字多次实例化
    # 如：var Pack = require('./mypackage').Package
    # 可通过：var pack_01 = new Pack(), pack_02 = new Pack(); 得到多个独立的实例
    exports.Package = Package;
     
    # 定义包的类和属性，注意不能通过“var Package = function() {}”的形式定义，否则出错
    function Package() {
        //定义类的属性
        this.name = 'MyName';
        //数组、列表的属性名称用复数
        this.tags = [];
        //私有属性名称前面加下划线
        this._secrect = '$%^&*43';
    }
     
    # 让包的类继承事件特性
    Package.prototype.__proto__ = EventEmitter.prototype;
     
    # 通过类的prototype定义类的方法
    Package.prototype.fun_01 = function() {
        //
    }
     
    Package.prototype.fun_02 = function() {
        //
    }
     
    # 用在类中但不暴露的通用方法可以定义在包的最后，名称前后用双下划线
    function __common_fun_01__() {
        //
    }
    
    
### 最简单的回调函数判断和执行

    function delay(time, cb) {
        
        setTimeout(function() {
            
            cb && cb(); // 前面的 cb 用于判断是否传递了这个参数，后边的 cb() 用于真正执行回调
        }
    }, time);
    
