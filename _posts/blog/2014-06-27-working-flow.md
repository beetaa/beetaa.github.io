---
layout: post
title: 工作流程
description: 流程化的工作，可以更快、更爽。
category: blog
---

### node环境自动化

1、nodemon 后台运行

    nohup nodemon server.js < /dev/null &
    # 如果不重定向到null, nodemon会马上退出
    
2、使用gulp