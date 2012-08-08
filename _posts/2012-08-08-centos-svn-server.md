---
layout: post
title: centos 6 64位服务器上搭建svn服务器
categories:
- linux
tags:
- tips
- svn
---

###centos 6 64位服务器上搭建svn服务器

>**SVN简介**  
　　subversion（简称svn）是近几年崛起的版本管理软件，是cvs的接班人，目前绝大多数开源软件都使用svn作为代码版本管理软件。Subversion支持linux和windows，但较多安装在linux下。
svn服务器有两种运行方式：独立服务器和借助于apache。 svn://或http://
####svn客户端tortoisesvn
**svn的基本工作原理： 在一台服务器上建立一个源代码库，库里可以存放许多不同项目的源程序。有源代码库管理员统一管理这些源程序。每个用户在使用源代码库之前，首先要把源代码库里德项目文件下载到本地，然后开发人员可以在本地修改，左后用svn命令进行提交，游源代码库统一管理修改。**
版本控制解决了：
*代码管理混乱
*解决代码冲突困难
*在代码整合期间引发bug
*无法对代码的拥有者进行权限控制
*项目不同版本的发布困难

过程记录 :

yum update 

**系统环境
CentOS 6.2  最小化安装
(关闭iptables和selinux) + ssh + yum**

setup 配置 网络及防火墙

###一，安装必须的软件包.
yum install subversion mysql-server httpd mod_dav_svn mod_perl sendmail wget gcc-c++ make unzip perl* ntsysv vim-enhanced

>说明：
subversion (SVN服务器)
mysql-server (用于codestriker)
httpd mod_dav_svn mod_perl (用于支持WEB方式管理SVN服务器)
sendmail (用于配置用户提交代码后发邮件提醒)
wget gcc-c++ make unzip perl* (必备软件包)
ntsysv vim-enhanced (可选)

###二，基本的SVN服务器配置
1，新建一个目录用于存储SVN所有文件
 >mkdir /home/svn

2，新建一个版本仓库
 >svnadmin create /home/svn/project

3，初始化版本仓库中的目录
 >mkdir project project/server project/client project/test (建立临时目录)
 svn import project/ file:///home/svn/project -m “初始化SVN目录”
 rm -rf project (删除临时建立的目录)

4，添加用户
要添加SVN用户非常简单，只需在/home/svn/project/conf/passwd文件添加一个形如“username=password”的条目就可以了。为了测试，我添加了如下内容:
>[users]
pm = pm_pw
server_group = server_pw
client_group = client_pw
test_group = test_pw

5，修改用户访问策略
/home/svn/project/conf/authz记录用户的访问策略，以下是参考:
>[groups]
project_p = pm
project_s = server1,server2,server3
project_c = client1,client2,client3
project_t = test1,test1,test1

>[project:/]
@project_p = rw
* =
>
[project:/server]
@project_p = rw
@project_s = rw
* =
>
[project:/client]
@project_p = rw
@project_c = rw
* =
>
[project:/doc]
@project_p = rw
@project_s = r
@project_c = r
@project_t = r
* =

以上信息表示，只有project_p用户组有根目录的读写权。r表示对该目录有读权限，w表示对该目录有写权限，rw表示对该目录有读写权限。

6，修改svnserve.conf文件,让用户和策略配置升效.
svnserve.conf内容如下:

>[general]
anon-access = none
auth-access = write
password-db = /home/svn/project/conf/passwd
authz-db = /home/svn/project/conf/authz

7，启动服务器
>svnserve -d -r /home/svn
注意：如果修改了svn配置，需要重启svn服务，步骤如下：

>ps -aux|grep svnserve
kill -9 ID号
svnserve -d -r /home/svn

8，测试服务器

>svn co svn://192.168.60.10/project
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Password for 'root':
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Username: server_group
Password for 'server_group':
svn: Authorization failed ( server_group没用根目录的访问权 )

> svn co svn://192.168.60.10/project
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Password for ‘root’:
Authentication realm: <svn://192.168.60.10:3690> 92731041-2dae-4c23-97fd-9e1ed7f0d18d
Username: pm
Password for ‘pm’:
A    project/test
A    project/server
A    project/client
Checked out revision 1.  ( 测试提取成功 )

 >cd project/server
 vim main.c
 svn add main.c
 svn commit main.c -m “测试一下我的C程序,看什么看,不行啊??”
Adding         main.c
Transmitting file data .
Committed revision 2.  ( 测试提交成功 )

自此 基本的 ＳＶＮ配置完了　更多的功能可以参考[（总结）CentOS Linux搭建SVN Server配置详解](http://www.ha97.com/4467.html)


###配置过程中出现的问题:

svn: 认证配置无效

URL 'svn://*.*.*.*>/project/wmct-dev' doesn't exist


[root@WMCT-PROJ svn]# svnadmin create ./wmct-dev
[root@WMCT-PROJ svn]# svnadmin create ./wmct-iot
[root@WMCT-PROJ svn]# svnadmin create ./wmct-cloud
[root@WMCT-PROJ svn]# svnadmin create ./wmct-public


需要把password-db = passwd前边的空格去掉，即password-db = passwd要顶行。
 
svn 认证失败

username = password

这是错误的，没空格，两边都没有
2.authz例子
只写
username = rw不足够
要写
[仓库名称:/]
username = rw

