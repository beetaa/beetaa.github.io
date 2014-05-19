---
layout: post
title: Markdown 简要指南
description: 忘了语法，打开这里，有一切需要。
category: blog
---


## 语法高亮-使用markdown缩进格式

源代码为:

```
语法高亮-使用markdown缩进格式:

   var fs = require('fs');
   
   function test(a, b) {
       return a + b;
   }
```

转换结果:

    var fs = require('fs');
    
    function test(a, b) {
        return a + b;
    }
    

## 图片-使用自带图片

源代码为：

```
![Joe Satriani](/images/guitarmaterial/joesatriani.jpg)
```

转换结果：

![Joe Satriani](/images/guitarmaterial/joesatriani.jpg)


## 图片-使用外链图片

```
![绿色植物]({{ site.media_url }}green-flower.png)
```

转换结果：

![绿色植物]({{ site.media_url }}green-flower.png)


