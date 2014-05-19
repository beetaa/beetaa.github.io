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

提示：方括号中的文字可以忽略，但方括号需要保留
```

转换结果：

![Joe Satriani](/images/guitarmaterial/joesatriani.jpg)


## 图片-使用外链图片

源代码为：

```
![绿色植物]({{ site.media_url }}green-flower.png)
```

转换结果：

![绿色植物]({{ site.media_url }}green-flower.png)


## 链接-书写中直接使用

源代码为：

```
[node.js](http://nodejs.com)
```

转换结果：

[node.js](http://nodejs.com)


## 链接-命名链接统一使用

### 1、将链接信息放置在文章最后

    [DNSPod]: http://dnspod.cn "DNSPod"
    [GitHub Pages]: http://pages.github.com "GitHub Pages"
    [WordPress]:    http://wordpress.org    "WordPress"
    [2]:  http://stevelosh.com/blog/2011/09/writing-vim-plugins/ "Write Vim Plugins"
    [3]: http://sivers.org/sharing   "The co-op business model: share whatever you've got"
    [4]: http://artificialrecords.com
    [5]: http://sivers.org/below-average    "probably below average"
    [6]: http://mindhacks.cn/2011/11/04/how-to-interview-a-person-for-two-years/    "怎样花两年时间去面试一个人"

### 2、后续即可在页面中这样引用

    我有一个 [DNSPod][DNSPod] 账号，跟 [GitHub][GitHub Pages] 关联，发
    表了一篇 [怎样花两年时间面试一个人][6] 的文章。

### 3、转换结果

我有一个 [DNSPod][DNSPod] 账号，跟 [GitHub][GitHub Pages] 关联，发表了一篇 [怎样花两年时间面试一个人][6] 的文章。



[DNSPod]: http://dnspod.cn "DNSPod"
[GitHub Pages]: http://pages.github.com "GitHub Pages"
[WordPress]:    http://wordpress.org    "WordPress"
[2]:  http://stevelosh.com/blog/2011/09/writing-vim-plugins/ "Write Vim Plugins"
[3]: http://sivers.org/sharing   "The co-op business model: share whatever you've got"
[4]: http://artificialrecords.com
[5]: http://sivers.org/below-average    "probably below average"
[6]: http://mindhacks.cn/2011/11/04/how-to-interview-a-person-for-two-years/    "怎样花两年时间去面试一个人"

