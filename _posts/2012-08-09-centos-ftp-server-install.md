---
layout: post
title: linux下FTP服务器搭建
categories:
- linux
tags:
- tips
- linux
---

###linux下FTP服务器搭建

yum install vsftpd

###2.启动/重启/关闭vsftpd服务器
[root@localhost ftp]# /sbin/service vsftpd restart
Shutting down vsftpd: [ OK ]
Starting vsftpd for vsftpd: [ OK ]
OK表示重启成功了.
启动和关闭分别把restart改为start/stop即可.
如果是源码安装的,到安装文件夹下找到start.sh和shutdown.sh文件,执行它们就可以了.

###3.与vsftpd服务器有关的文件和文件夹
vsftpd服务器的配置文件的是: /etc/vsftpd/vsftpd.conf

vsftpd服务器的根目录,即FTP服务器的主目录:
在/var/ftp处pub处
如果你想修改服务器目录的路径,那么你只要修改/var/ftp到别处就行了

###4.添加FTP本地用户
有的FTP服务器需要用户名和密码才能登录,就是因为设置了FTP用户和权限.
FTP用户一般是不能登录系统的,只能进入FTP服务器自己的目录中,这是为了安全.这样的用户就叫做虚拟用户了.实际上并不是真正的虚拟用户,只是不能登录SHELL了而已,没能力登录系统.

/usr/sbin/adduser -d /opt/test_ftp -g ftp -s /sbin/nologin test
/usr/sbin/adduser -d /var/ftp/wmct -g ftp -s /sbin/nologin wmctftp

###取消禁用root用户: 
确认/etc/vsftpd.ftpusers中无root行，或#root。 
确认/etc/vsftpd.user_list中无root行，或#root。 


这个命令的意思是:
使用命令(adduser)添加test用户,不能登录系统(-s /sbin/nologin),自己的文件夹在(-d /opt/test_ftp)),属于组ftp(-g ftp)
然后你需要为它设置密码 passwd test
这样就添加了一个FTP用户了.下面的示例可以帮助你进入FTP服务器了.

[root@localhost ftp]# ftp
ftp> open 192.168.0.33
Connected to 192.168.0.33 (192.168.0.33).
220 (vsFTPd 2.0.5)
Name (192.168.0.33:gxl): test
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> quit
221 Goodbye.

在windows中,只要在浏览器中输入 ftp://192.168.0.33 进入FTP服务器,然后 右键 登录,输入用户名和密码就可以登录自己的目录了.
当然你要保证自己能读写自己的目录,就要在配置文件vsftpd.conf里设置一下就可以读写了.
local_enable=yes
write_enable=yes
local_umask=022

###5.匿名上传下载
修改配置文件即可vsftpd.conf,确定有以下几行,没有自己添加进去就可以了.
anonymous_enable=yes
anon_upload_enable=yes
anon_mkdir_write_enable=yes
anon_umask=022

然后你可以新建一个文件夹,修改它的权限为完全开放,任何用户就可以登录这个文件夹,并上传下载文件:
mkdir /var/ftp/guest
chmod 777 /var/ftp/guest

###6.定制进入FTP服务器的欢迎信息
在vsftpd.conf文件中设置:
dirmessage_enable=yes
然后进入用户目录建立一个.message文件,输入欢迎信息即可(我这里写入的是Welcome to gxlinux's FTP!):
[root@localhost test_ftp]# ftp 192.168.0.33
Connected to 192.168.0.33 (192.168.0.33).
220 (vsFTPd 2.0.5)
Name (192.168.0.33:gxl): test
331 Please specify the password.
Password:
230-Welcome to gxlinux's FTP!
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

###7.实现虚拟路径
将某个目录挂载到FTP服务器下供用户使用,这就叫做虚拟路径.
比如将gxl用户的目录挂载到FTP服务器中,供FTP服务器的用户使用,使用如下命令即可:
[root@localhost opt]# mount --bind /home/gxl /var/ftp/pub #使用挂载命令
[root@localhost opt]# ls /var/ftp/pub
LumaQQ Screenshot.png 桌面

###8.打开vsFTPd的日志功能
添加下面一行到vsftpd.conf文件中,一般情况下该文件中有这一行,只要把前面的注释符号#去掉即可,没有的话就添加,或者修改:
xferlog_file=/var/log/vsftpd.log

###9.限制链接数,以及每个IP最大的链接数
修改配置文件中,例如vsftp最大支持链接数100个,每个IP能支持5个链接:
max_client=100
max_per=5

###10.限制传输速度
修改配置文件中,例如让匿名用户和vsftd上的用户(即虚拟用户)都以80KB=1024*80=81920的速度下载
anon_max_rate=81920
local_max_rate=81920

###11.将用户(一般指虚拟用户)限制在自家目录
修改配置文件中,这样用户就只能访问自己家的目录了:
chroot_local_user=yes
如果只想某些用户仅能访问自己的目录,其它用户不做这个限制,那么就需要在chroot_list文件(此文件一般是在/etc/vsftpd/中)中添加此用户.
编辑此文件,比如将test用户添加到此文件中,那么将其写入即可.一般的话,一个用户占一行.
[root@localhost vsftpd]# cat chroot_list
test

###12.绑定某个IP到vsFTPd
有时候要限制某些IP访问服务器,只允许某些IP访问,例如只允许192.168.0.33访问这个FTP,同样修改配置文件:
listen_address=192.168.0.33


配置vsftpd.conf
                 > anonymous_enable=NO            #禁止匿名
                   local_enable=YES                       #允许本地登录
                   write_enable=YES                       #允许写，如需上传，则必须
                   local_umask=027                        #将上传文件的权限设置为：777-local_umask
                   anon_upload_enable=YES          #允许虚拟用户和匿名用户上传
                   anon_other_write_enable=YES #允许虚拟用户和匿名用户修改文件名和删除文件
                   dirmessage_enable=YES           
                   xferlog_enable=YES                      #打开日志记录
                   connect_from_port_20=YES
                   xferlog_file=/var/log/vsftpd.log     #日志存放位置
                   xferlog_std_format=YES              #标准日志格式
                   idle_session_timeout=600        #空闲连接超时
                   data_connection_timeout=120
                   ftpd_banner=Welcome to ChinaRise FTP service       #欢迎信息
                   guest_enable=yes                       #允许虚拟用户
                   guest_username=vsftpdguest #虚拟用户使用的系统账号
                   virtual_use_local_privs=YES     #虚拟用户拥有本地系统权限
                   chroot_local_user=NO              
                   chroot_list_enable=YES
                     #以上两行将虚拟用户限制在其目录下，不能访问其他目录，或者直接用                            
                   chroot_local_user=YES                               
                   listen=yes                #监听/被动模式
                   listen_port=21        #监听端口
                   chroot_list_file=/etc/vsftpd/vsftpd.chroot_list       #虚拟用户名单保存在文件/etc/vsftpd/vsftpd.chroot_list 中
                   user_config_dir=/etc/vsftpd/vsftpd_user_conf   #每个虚拟用户名的更加详细的培植保存在/etc/vsftpd/vsftpd_user_conf 中

###虚拟用户其他设置

      在/etc/vsftpd/vsftpd.chroot_list 文件中写入允许登陆的虚拟用户名称，每行一个
      在/etc/vsftpd/vsftpd_user_conf 文件夹中创建一个以虚拟用户用户名命名的文件，
      写入：local_root = /var/FTP/子目录名
      然后在/var/FTP下创建一个对应的目录即可

###Vsftpd虚拟用户

步骤：
1.建立虚拟用户口令库文件
2.生成vsftpd的认证文件  （/etc/pam.d/vsftpd/)
3.建立虚拟用户所需的PAM配置文件
4.建立虚拟用户所需访问的目录并设置相应权限
5.设置vsftpd.conf配置文件


