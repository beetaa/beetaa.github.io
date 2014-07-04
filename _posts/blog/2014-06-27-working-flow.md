---
layout: post
title: 工作流程
description: 流程化的工作，可以更快、更爽。
category: blog
---

### node环境自动化

1、nodemon 后台运行

```sh
> nohup nodemon server.js < /dev/null &
# 如果不重定向到null, nodemon会马上退出
```
    
2、使用gulp.js

### 测试环境自动化

1、使用 pageres 抓取页面的不同分辨率渲染结果

```sh
> sudo npm install -g pageres
> pageres [ beetaa.com 1280x800 1024x768 800x600 ] --crop
```

pageres@[github](https://github.com/sindresorhus/pageres)。
pageres还可以和[grunt.js](https://github.com/sindresorhus/grunt-pageres)一起使用。
