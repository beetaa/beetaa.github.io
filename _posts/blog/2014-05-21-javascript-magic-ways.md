---
layout: post
title: Javascript 技巧小集
description: 一些 JS 编程小技巧、小片段，不惊世，不骇俗，关键要实用
category: blog
---

## 最简单的回调函数判断和执行

    function delay(time, cb) {
        
        setTimeout(function() {
            
            cb && cb();
        }
    }, time);
    
