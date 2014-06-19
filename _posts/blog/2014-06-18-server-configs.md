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
    
    # 如果使用putty登录，则先使用puttygen.exe转换密钥
    
    # 设置ssh保持连接
    # 1 - 服务器端
    > sudo gedit /etc/ssh/sshd_config 设置 ClientAliveCountMax 600
    > sudo /etc/init.d/sshd restart
    # 2 - 客户端
    > sudo gedit /etc/ssh/ssh_config 设置 ServerAliveInterval 60
    
    # 创建并使用swap分区 - 少量多个，不要放在/tmp目录下
    > sudo mkdir /var/swap
    > dd if=/dev/zero of=/var/swap/swap01 bs=1M count=1024
    mkswap -f /var/swap/swap01
    sudo swapon /var/swap/swap01
    sudo vim /etc/fstab 添加一行 /var/swap/swap01  swap  swap  defaults  0  0
    # 重复上述步骤可创建多个swap分区
    
    # 安装基本软件和编译库
    > sudo apt-get install python php-cli git curl unrar unzip
    > sudo apt-get install python-dev python-software-properties python-setuptools
    > sudo apt-get install build-essential g++ gcc make automake autoconf libgtk2.0-dev
    > sudo apt-get install python-openssl python-crypto
    # 以下python库可选
    > sudo apt-get install python-greenlet python-gevent python-vte python-appindicator
    
### 配置通过mail命令发送邮件

    # 安装
    > sudo apt-get install ssmtp mailutils
    
    # 配置 ssmtp
    > sudo vim /etc/ssmtp/ssmtp.conf
    # 设置以下内容
    root=用户名@gmail.com
    mailhub=smtp.gmail.com:465
    rewriteDomain=gmail.com
    AuthUser=邮箱账户名
    AuthPass=邮箱密码
    hostname=服务器名称
    FromLineOverride=YES
    UseTLS=YES
    
    # 两种方法发送邮件
    > echo "Hi, This is mail from test server" | mail -s "test mail from test server" MAIL_TO_SEND@DOMAIN
    > mail -s "这是邮件标题" foyo23@zhuidaniu.com < body.txt
    

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