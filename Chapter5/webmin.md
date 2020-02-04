#  第 1 节 安装主机控制面板(可选)

就称为“主机控制面板”吧.

主机控制面板,是管理linux系统的可视化工具.我以前用过Vesta Control Panel,zcz用的webmin.看了一眼,可能webmin更好用...

### 2 安装webmin

1）下载webmin
http://www.webmin.com/download.html
2）安装perl依赖
yum -y install perl perl-Net-SSLeay openssl perl-IO-Tty perl-Encode-Detect perl-Data-Dumper
3）安装webmin
rpm -Uvh webmin-1.910-1.noarch.rpm
4）设置开机启动
文件中：/etc/rc.d/rc.local
加入：/etc/webmin/start
5）访问webmin
https://localhost.localdomain:10000/init/?xnavigation=1



### 3 安装Vesta Control Panel

安装步骤从库存中取来

1）登录问题

```
ssh ubuntu@139.199.9.173
ubuntu@139.199.9.173's password:
重装系统以后无法登录。
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
rm /Users/XXX/.ssh/known_hosts 就可以登录了。
```

2）安装

2.1）

```json
curl -O http://vestacp.com/pub/vst-install.sh
// linux中,curl是命令行下的http文件传输工具,支持文件的上传和下载。
// 语法：# curl [option] [url]
// -O/--remote-name 把输出写到该文件中，保留远程文件的文件名
```

2.2）

```
bash vst-install.sh
Error: this script can only be executed by root
```



用root登录的话     

```json
$ sudo su passwd root
$ vi /etc/ssh/sshd_config // 把里面那行PermitRootLogin删掉
```



### 2.3）

```
sudo bash vst-install.sh``[sudo] password ``for` `ubuntu:
```

　　

```
Following software will be installed ``on` `your system:``  ``- Nginx Web Server``  ``- Apache Web Server (``as` `backend)``  ``- Bind DNS Server``  ``- Exim mail server``  ``- Dovecot POP3/IMAP Server``  ``- MySQL Database Server``  ``- Vsftpd FTP Server``  ``- Iptables Firewall + Fail2Ban
```

　Please enter admin email address: 156463617@qq.com

  Please enter FQDN hostname [localhost]: localhost

  Congratulations, you have just successfully installed Vesta Control Panel

### 2.4)

然后通过网站登录，https://10.135.XX.XX:8083

username: admin
password: XXXX

###  3) 错误解决

前台创建的mysql，在后台能使用用户登录，前台则无法登录phpMyAdmin

/etc/phpmyadmin/config.inc.php

修改用户名、密码

$cfg['Servers'][$i]['controluser'] = '';

$cfg['Servers'][$i]['controlpass'] = '';

重启vesta

 sudo  service vesta restart