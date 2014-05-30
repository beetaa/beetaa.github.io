---
layout: post
title: 有关那道“墙”的记忆
description: 我们只是听话的小孩子，我们只想学习先进的技术，何必为难我们？
category: blog
---

### npm国内镜像

- 淘宝：``http://registry.npm.taobao.org``
- cnpm：``http://registry.cnpmjs.org``
- 官方库：``https://registry.npmjs.org``

    # 临时
    npm config set registry http://registry.cnpmjs.org
    # 临时
    npm --registry http://registry.cnpmjs.org info underscore
    # 永久
    编辑 .npmrc 文件，加入 registry = http://registry.cnpmjs.org
    


[Beetaa]:    http://beetaa.com  "Beetaa"
