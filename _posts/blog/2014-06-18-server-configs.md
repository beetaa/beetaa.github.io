---
layout: post
title: 服务器配置备忘
description: 走过的弯路，以后不要再走。
category: blog
---

### 基本环境

    # 修改命令提示符
    > gedit ~/.bashrc
    
    # 修改软件源
    > sudo gedit /etc/apt/sources.list
    
    # 配置ssh密钥登录
    # 1 - 将本地 ~/.ssh/id_dsa.pub 复制到服务器
    # 2 - 将上述的key内容添加到服务器端的 ~/.ssh/authorized_keys 文件中
    # 3 - 设置权限
    # 4 - 服务器端ssh配置文件，打开密钥认证选项
    > scp ~/.ssh/id_rsa.pub user@remote.host:pubkey.txt
    > ssh user@remote.host
    > cat pubkey.txt >> ~/.ssh/authorized_keys
    > chmod 700 ~/.ssh
    > chmod 600 ~/.ssh/*
    > sudo gedit /etc/ssh/ssh_config 设置 PubkeyAuthentication yes

### vsftpd的安装和配置

    # 安装
    > sudo apt-get install vsftpd
    
    # 配置
    > sudo vim /etc/vsftpd.conf
    
    anonymous_enable=NO    # 默认可以匿名登录
    local_enable=YES        # 使用本地用户名和密码登录
    write_enable=YES        # 可以上传文件
    local_umask=022         # 上传文件默认权限
    
    # 用户组、登录用户和目录
    > groupadd ftp-users
    > mkdir /var/ftp
    > chmod 775 /var/ftp    # 此处权限要够，否则登不进去
    > chown root:ftp-users /var/ftp     # 设置文件夹归属
    > useradd -g ftp-users -d /var/ftp user1    # 添加用户并设置用户目录
    > passwd user1  # 设置用户密码
    
    # 重启
    > sudo /etc/init.d/vsftpd restart
    # 或
    > sudo service vsftpd restart