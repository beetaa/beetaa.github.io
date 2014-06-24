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
    
    # 安装基本软件和编译库
    > sudo apt-get install python php-cli git curl unrar unzip
    > sudo apt-get install python-dev python-software-properties python-setuptools
    > sudo apt-get install build-essential g++ gcc make automake autoconf libgtk2.0-dev
    > sudo apt-get install python-openssl python-crypto
    # 以下python库可选
    > sudo apt-get install python-greenlet python-gevent python-vte python-appindicator
    
### 配置ssh通过密钥登录并可保持长连接

    # 本地客户端操作
    > ssh-keygen -t rsa # 生成key对
    > scp ~/.ssh/id_rsa.pub user@remote.host:pubkey.txt # 将公钥上传至服务器
    > sudo gedit /etc/ssh/ssh_config    # 设置 ServerAliveInterval 60
    
    # 服务器端操作
    > cat pubkey.txt >> ~/.ssh/authorized_keys
    > chmod 700 ~/.ssh
    > chmod 600 ~/.ssh/ *
    > sudo vim /etc/ssh/ssh_config      # 设置 PubkeyAuthentication yes
    > sudo vim /etc/ssh/sshd_config     # 设置 ClientAliveCountMax 600
    > sudo /etc/init.d/sshd restart
    
    # 如果客户端使用putty登录，则先使用puttygen.exe将密钥转换为ppk格式
    
### 创建并使用swap分区
    
    > sudo mkdir /var/swap
    > dd if=/dev/zero of=/var/swap/swap01 bs=1M count=1024
    > mkswap -f /var/swap/swap01
    > sudo swapon /var/swap/swap01
    > sudo vim /etc/fstab 添加一行 /var/swap/swap01  swap  swap  defaults  0  0
    
    # 重复上述步骤可创建多个swap分区
    # swap分区要少量多个，而且不要放在/tmp目录下
    
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
    
### pptpd vpn 服务器安装和配置

    # 验证是否开启ppp
    > cat /dev/ppp
    # 成功标志：cat: /dev/ppp: No such file or directory 
    # 失败标志：cat: /dev/ppp: Permission denied，请联系vps服务商开启。
    
    # 验证开启tun/tap，如果只用pptp方式，则不需要
    > cat /dev/net/tun
    # 成功标志：
    
    # 安装pptpd、iptables
    > sudo apt-get install pptpd iptables
    
    # 配置/etc/pptpd.conf
    > sudo vim /etc/pptpd.conf
    # 修改或添加以下两行
    localip 192.168.0.1
    remoteip 192.168.0.234-238,192.168.0.245
    # 其中localip为vpn服务器用到的网址
    # remoteip为客户端可用的ip地址，可以是地址范围
    
    # 配置/etc/ppp/pptpd-options
    > sudo vim /etc/ppp/pptpd-options
    # 修改或添加dns配置
    ms-dns 8.8.8.8
    ms-dns 8.8.4.4
    
    # 配置登录用户和密码
    > sudo vim /etc/ppp/chap-secrets
    # 每行一个用户信息（用户名 服务器名 密码 ip限制），如：
    user pptpd password *
    # 建议多配置几个，用自己的客户端命名，如T60P, Meizu等
    
    # 开启 ipv4 forward
    > sudo vim /etc/sysctl.conf
    # 去掉 #net.ipv4.ip_forward=1 前的 # 号
    > sudo sysctl -p
    # 如果显示 net.ipv4.ip_forward = 1 则表示已生效
    
    # 配置iptables转发并自让其随系统启动
    > sudo vim /etc/rc.local
    # 添加以下内容
    iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -j SNAT --to-source VPN服务器的公网IP
    # 192.168.0.0 要和 /etc/pptpd.conf 中的地址段一致
    # 24是掩码，代表24个1
    # --to-source 后面是VPN服务器的公网IP
    > chmod +x /etc/rc.local
    
    # 重启系统
    > reboot
    
**常见问题及解决**

* Cannot determine ethernet address for proxy ARP
> dns的设置问题，检查/etc/resolve.conf配置文件与/etc/ppp/option文件中的dns server的设置。
    