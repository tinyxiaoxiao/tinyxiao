---
layout: post
title: CentOS linux 系统建立Vsftpd虚拟用户
categories:
- linux
tags:
- tips
- linux
---

### 建立Vsftpd虚拟用户
参照 http://yuanbin.blog.51cto.com/363003/129071/
脚本 http://feixiang123.blog.51cto.com/285543/75839/


Vsftpd虚拟用户

步骤：
1.建立虚拟用户口令库文件
2.生成vsftpd的认证文件  （/etc/pam.d/vsftpd/)
3.建立虚拟用户所需的PAM配置文件
4.建立虚拟用户所需访问的目录并设置相应权限
5.设置vsftpd.conf配置文件


一、本地数据文件方式
1. 添加虚拟用户口令文件
[root@CentOS5 /]#vi /etc/vsftpd/vftpuser.txt
添加虚拟用户名和密码，一行用户名，一行密码，以此类推。奇数行为用户名，偶数行为密码。
bobyuan #用户名
123456 #密码
markwang #用户名
123456 #密码
 
2. 生成虚拟用户口令认证文件
将刚添加的vftpuser.txt虚拟用户口令文件转换成系统识别的口令认证文件。
首先查看系统有没有安装生成口令认证文件所需的软件db4-utils。
[root@CentOS5 /]#rpm –qa |grep db4-utils
[root@CentOS5 /]#rpm –ivh db4-utils-4.3.29-9.fc6.i386.rpm
下面使用db_load命令生成虚拟用户口令认证文件。
[root@CentOS5 /]#db_load –T –t hash –f /etc/vsftpd/vftpuser.txt /etc/vsftpd/vftpuser.db
 
3. 编辑vsftpd的PAM认证文件
在/etc/pam.d目录下，
[root@CentOS5 /]#vi /etc/pam.d/vsftpd
将里面其他的都注释掉，添加下面这两行：
auth required /lib/security/pam_userdb.so db=/etc/vsftpd/vftpuser
account required /lib/security/pam_userdb.so db=/etc/vsftpd/vftpuser
 
4. 建立本地映射用户并设置宿主目录权限
所有的FTP虚拟用户需要使用一个系统用户，这个系统用户不需要密码。
[root@CentOS5 /]#useradd –d /home/vftpsite –s /sbin/nologin vftpuser
[root@CentOS5 /]#chmod 700 /home/vftpsite
 
5. 配置vsftpd.conf（设置虚拟用户配置项）
[root@CentOS5 /]#vi /etc/vsftpd/vsftpd.conf
guest_enable=YES #开启虚拟用户
guest_username=vftpuser #FTP虚拟用户对应的系统用户
pam_service_name=vsftpd #PAM认证文件
 
6. 重启vsftpd服务
[root@CentOS5 /]#service vsftpd restart
 
7. 测试虚拟用户登录FTP
C:\User\Administrator>ftp 192.168.120.240
连接到192.168.120.240。
220 Welcome to BOB FTP server
用户(192.168.120.240(none)):markwang
331 Please specify the password.
密码:
230 Login successful.

###生成脚本

//#!/bin/sh
####添加虚拟的用户帐户！
touch /tmp/ftpuser_list
echo "feixiang
1985731
" >/tmp/ftpuser_list
rm -rf /etc/vsftpd_login.db
db_load -T -t hash -f /tmp/ftpuser_list /etc/vsftpd_login.db
chmod 600 /etc/vsftpd_login.db
touch /etc/pam.d/ftp.vu
echo "auth required /lib/security/pam_userdb.so db=/etc/vsftpd_login
account required /lib/security/pam_userdb.so db=/etc/vsftpd_login" >/etc/pam.d/ftp.vu
####添加本地计算机用户名和密码；
useradd -d /ftp -s /sbin/nologin vsftp
chown -R vsftp.vsftp /ftp
touch /tmp/new_ftppwd
echo "vsftp:1985731" >/tmp/new_ftppwd
chpasswd < /tmp/new_ftppwd
####配置vsftpd.conf全局设置：
cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.bak.00
echo "anonymous_enable=NO
anonymous_enable=NO
####本地帐户配置！
local_enable=YES
local_umask=022
dirmessage_enable=YES
connect_from_port_20=YES
####启用来宾帐号，也就是虚拟用户使用的帐号的权限用户。
guest_enable=YES
guest_username=vsftp
user_config_dir=/etc/vsftpd/user_config_dir
local_root=/www
write_enable=YES
pam_service_name=ftp.vu
userlist_enable=YES
listen=YES
chroot_local_user=YES
tcp_wrappers=YES
####ftp用户日志配置！(双日志方案！)
xferlog_enable=YES
xferlog_std_format=YES
xferlog_std_format=YES
xferlog_file=/var/log/xferlog
dual_log_enable=YES
vsftpd_log_file=/var/log/vsftpd.log" >/etc/vsftpd/vsftpd.conf
####配置虚拟用户名的设置：
mkdir -p /etc/vsftpd/user_config_dir
mkdir -p /www/feixiang
chmod -R 777 /www/feixiang
touch /etc/vsftpd/user_config_dir/feixiang
echo "anon_world_readable_only=NO
write_enable=YES
anon_upload_enable=YES
anon_other_write_enable=YES
local_root=/www/feixiang
anon_mkdir_write_enable=YES" >/etc/vsftpd/user_config_dir/feixiang
####重启vsftpd服务器，就OK了。
service vsftpd restart
####feixiang 这个帐户，就弄好了。


如果你要添加新的虚拟用户，可以在这个文件里面加入新的用户：
/tmp/ftpuser_list然后保存。（注意ftpuser_list的格式。）
feixiang #用户名
1985731  #密码
username #用户名
passwd   #密码
记住中间没有空行和空格。
再使用：
rm -rf /etc/vsftpd_login.db
db_load -T -t hash -f /tmp/ftpuser_list /etc/vsftpd_login.db
就可以添加新的用户了。添加新用户后：不用重启服务，就可以生效了。