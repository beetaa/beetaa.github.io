---
layout: post
title: Markdown 简要指南
description: 忘了语法，打开这里，有一切需要。
category: blog
---

#语法高亮 - 使用 markdown 缩进格式

源代码为

```

    语法高亮 - 使用 markdown 缩进格式:
    
        var fs = require('fs');
        
        function test(a, b) {
            return a + b;
        }
        
```

源代码为

>     语法高亮 - 使用 markdown 缩进格式:
    
        var fs = require('fs');
        
        function test(a, b) {
            return a + b;
        }


转换结果:

    var fs = require('fs');
    
    function test(a, b) {
        return a + b;
    }

#语法高亮 - 使用 jekyII 模板语言


![Joe Satriani](/images/guitarmaterial/joesatriani.jpg)

Hello World! {{ site.media_url }}, that's good.

![绿色植物]({{ site.media_url }}green-flower.png)

{% highlight js %}

var fs = require('fs');

function test(a, b) {
    return a + b;
}

{% endhighlight %}
