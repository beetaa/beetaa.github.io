---
layout: post
title: 项目工作环境配置
description: 完美主义者的工作台，需要诸多出乎意料的创新小配置。
category: blog
---

### 一、利用 Dropbox + Git 维护代码仓库

1、实现原理：

    +------------+            +-----------+              +---------+
    |  Dropbox   |  --Sync->  |  Dropbox  |   --Clone->  | Working |
    |   Server   |  <-Sync--  |   Client  |   <-Push---  |  Space  |
    +------------+            +-----------+              +---------+

2、实现步骤：

    # 初始化本地代码库
    ~/project $ git init
    ~/project $ git add .
    ~/project $ git commit -m "first commit"
    
    # 在 Dropbox 中创建 Git 仓库
    ~/project $ cd ~/Dropbox/git
    ~/Dropbox/git $ git init --bare project.git
    
    # 将本地仓库关联并推送至 Dropbox 仓库
    ~/Dropbox/git $ cd ~/project
    ~/project $ git remote add origin ~/Dropbox/git/project.git
    ~/project $ git push -u origin master
    
    # 如果是windows下，路径格式为：file:///e:/sync/dropbox/git/server.git
    
3、错误解决：

    # 删除 Git 仓库，重建同名的仓库
    $ cd ~/Dropbox/git
    $ rm -rf project.git
    $ git init --bare project.git
    
    # 将保存最新代码的本地仓库 push 回去
    $ git push origin master
    
4、参考文档：

* [Using Git and Dropbox together effectively?](http://stackoverflow.com/questions/1960799/using-git-and-dropbox-together-effectively)
* [Using Dropbox as a Private GitHub](http://jetheis.com/blog/2013/02/17/using-dropbox-as-a-private-github/)

### 二、用 gulp.js 实现自动化操作

1、安装gulp.js

    # 全局安装
    npm install -g gulp
    # 工程中安装
    npm install --save-dev gulp
    # 安装插件
    npm install --save-dev gulp-util gulp-uglify gulp concat

参考：[gulp.js 插件清单](http://gulpjs.com/plugins/)

2、用task、run、watch、src、dest构建gulpfile.js任务

    // 引入 gulp
    var gulp = require('gulp');
    
    // 引入 插件
    var compass = require('gulp-compass');
    
    // 创建 Compass 任务
    gulp.task('compass', function() {
      gulp.src('./scss/**')
        .pipe(compass({
            comments: false,
            css: 'css',
            sass: 'scss',
            image: 'img'
        }));
    });
    
    // 配置默认运行的任务
    gulp.task('default', function() {
        gulp.run('compass');
    
        gulp.watch([
            './scss/**',
            './img/**'
            ], function(event) {
            gulp.run('compass');
        });
    });
    
3、gulp.js流程图

![gulp流程图](/images/workbenchconfigs/gulp.png)

4、gulp.js插件框架

    // through2 模块是对 node stream 的包装
    var through = require('through2');
    var gutil = require('gulp-util');
    var PluginError = gutil.PluginError;
    
    // 定义常数，这里是插件的名称
    const PLUGIN_NAME = 'gulp-prefixer';
    
    // 通过 through 初始化读写流
    function prefixStream(prefixText) {
      var stream = through();
      stream.write(prefixText);
      return stream;
    }
    
    // 插件功能主函数（处理文件数据）
    function gulpPrefixer(prefixText) {
    
      if (!prefixText) {
        throw new PluginError(PLUGIN_NAME, "Missing prefix text!");
      }
      prefixText = new Buffer(prefixText); // allocate ahead of time
    
      // Creating a stream through which each file will pass
      var stream = through.obj(function(file, enc, callback) {
        // 如果文件内容为空，则忽略
        if (file.isNull()) {
           
        }
        // 如果文件内容为buffer，则使用cancat方法
        if (file.isBuffer()) {
            file.contents = Buffer.concat([prefixText, file.contents]);
        }
        // 如果文件内容为流，则使用pipe方法
        if (file.isStream()) {
            file.contents = file.contents.pipe(prefixStream(prefixText));
        }
    
        this.push(file);
        return callback();
    
      });
    
      // 返回读写流
      return stream;
    };
    
    // 导出主功能函数
    module.exports = gulpPrefixer;

参考：[Writing a plugin](https://github.com/gulpjs/gulp/blob/master/docs/writing-a-plugin/README.md)

5、参考：

* [Gulp.js—比Grunt更易用的前端构建工具](http://www.36ria.com/6373)
* [Gulp.js深入讲解](http://www.36ria.com/6382)



[Beetaa]:    http://beetaa.com  "Beetaa"
