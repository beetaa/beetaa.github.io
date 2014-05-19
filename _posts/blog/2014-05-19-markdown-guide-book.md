---
layout: post
title: Markdown 简要指南
description: 忘了语法，打开这里，有一切需要。
category: blog
---

## 基本语法

- 黑体：在需要着重的词句前后使用 `**`，如 `**node.js**` 的效果就是 **node.js**
- 横线：`<hr>` 或 `---`
- 支持的html标记：`<ul>` | `<li>` | `<ol>` | `<pre>` | `<code>` | `<hr>` | `<br>`
- 引用：使用 `> `，记住 `>` 应紧跟一个**空格**或**制表符**，引用可以 **嵌套**，如：`>> ` 或 `>>> `
- 列表：无需列表使用 `* ` | `+ ` | `- `，同样应紧跟一个**空格**或**制表符**；有序列表使用 `1. ` 的格式，数字的**先后**和**顺序**都无所谓
- 列表和引用均支持段落式块状内容
- 一般链接：`[百度](http://www.baidu.com)` 将转换为 [百度](http://www.baidu.com)
- 直接链接：`<http://www.baidu.com>` 将转换为 <http://www.baidu.com>，可以用于邮件地址，如：`<somebody@github.com>`
- 图片：`![Joe Satriani](/images/guitarmaterial/joesatriani.jpg)` 或 `![绿色植物]({{ site.media_url }}green-flower.png)`

## 语法高亮

源代码为:

```
语法高亮-使用markdown缩进格式:

'   var fs = require('fs');
    
'   function test(a, b) {
'       return a + b;
'   }
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

