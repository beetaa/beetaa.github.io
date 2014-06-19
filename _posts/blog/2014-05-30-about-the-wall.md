---
layout: post
title: 有关那道“墙”的记忆
description: 我们只是听话的小孩子，我们只想学习先进的技术，何必为难我们？
category: blog
---

### 一、npm国内镜像

- 淘宝：``http://registry.npm.taobao.org``
- cnpm：``http://registry.cnpmjs.org``
- 官方库：``https://registry.npmjs.org``

设置方法

    npm config set registry http://registry.cnpmjs.org  #临时生效
    npm --registry http://registry.cnpmjs.org info underscore   #临时生效
    编辑 .npmrc 文件，加入 registry = http://registry.cnpmjs.org    #永久生效
    
### 二、openshift + tunnelizer

- openshift生成app的ssh访问url，含主机地址+用户名
- 本地keygen密钥对，将公钥上传到openshift
- 从 [Tunnelizer官网][Tunnelizer官网] 或 [百度网盘][百度网盘] 下载 ``Tunnelizer``
- login 标签 - 填入主机地址、用户名
- login 标签 - 点击 ``user keypair manager`` 导入私钥，并从用户名下面的下拉框
  中选择 ``publickey - slot 1``
- services 标签 - enabled sock，根据需要填入端口号
- options 标签 - 取消 ``open terminal`` 和 ``open sftp``
- 保存配置的 profile
- 开机启动并最小化：在快捷方式属性中修改为 ``"tunnelizer.exe" -profile=something.tlp -loginOnStartup``
- ok

- 如果dns污染，可通过ip138等反查主机地址的ip，写入系统 ``host`` 文件

参考：[OpenShift SSH fq 教程](https://zero-rufeng.rhcloud.com/?p=21)


[Beetaa]: http://beetaa.com  "Beetaa"
[Tunnelizer官网]: http://www.bitvise.com/download-area
[百度网盘]: http://pan.baidu.com/share/link?shareid=107155&uk=2584079325
