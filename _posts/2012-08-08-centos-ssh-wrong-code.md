---
layout: post
title: CentOS系统中文乱码
categories:
- linux
tags:
- tips
- linux
---
###CentOS系统中文乱码 经常会碰到下面是 各种解决方法：

>在使用CentOS系统时，安装的时候可能你会碰到英文的CentOS系统，在这中情况下安装CentOS系统时是默认安装（即英文）。安装完毕后，出现的各种中文乱码。那么，我们如何解决这种问题呢。

####一、CentOS系统访问 g.cn ，发现中文乱码。
>于是用以前的方式：yum -y install fonts-chinese
CentOS系统安装后，还是不能显示中文字体。我使用 gedit 编辑源码，其中文注释也为乱码。
后来，终于找到以下方法可以解决，需要两个中文支持的包：
fonts-chinese-3.02-12.el5.noarch.rpm
ftp://ftp.muug.mb.ca/mirror/centos/5.4/os/x86_64/CentOS/fonts-chinese-3.02-12.el5.noarch.rpm
fonts-ISO8859-2-75dpi-1.0-17.1.noarch.rpm
ftp://ftp.muug.mb.ca/mirror/centos/5.4/os/x86_64/CentOS/fonts-ISO8859-2-75dpi-1.0-17.1.noarch.rpm
一个是中文字体，一个是字体显示包。
下载后，在命令行安装：
rpm -ivh XXXX （ XXXX 代表上面那两个包的全名， rpm 不会不知道怎么用吧？）
CentOS系统安装完成后，重新启动即可。

###二、终端、 gedit 显示乱码
vi /etc/sysconfig/i18n
将LANG="en_US.UTF-8"
SYSFONT="latarcyrheb-sun16"
修改原内容为
LANG="zh_CN.GB18030"
LANGUAGE="zh_CN.GB18030:zh_CN.GB2312:zh_CN"
SUPPORTED="zh_CN.UTF-8:zh_CN:zh:en_US.UTF-8:en_US:en"
SYSFONT="lat0-sun16"
用 yum 安装中文字体
yum install fonts-chinese.noarch
system  ->  logout  注销
重新登录CentOS系统时，你会发现，所有界面已从英文变成中文。在终端输入 date 命令测试
date

###三、在 ssh ， telnet 终端中文显示乱码解决办法（ CentOS 5.3 ）
vi /etc/sysconfig/i18n
将原内容 LANG="en_US.UTF-8"
SYSFONT="latarcyrheb-sun16"
修改为
LANG="zh_CN.GB18030"
LANGUAGE="zh_CN.GB18030:zh_CN.GB2312:zh_CN"
SUPPORTED="zh_CN.UTF-8:zh_CN:zh:en_US.UTF-8:en_US:en"
SYSFONT="lat0-sun16"

断开 ssh ，重新连
在终端输入 date 命令测试
date

###四、在CentOS系统 5.3 中使用中文输入法
我以前的方法是安装企鹅版 ，见下一页 。 在此，还有一个更简单的，只要使用 yum 安装 SCIM 即可。
命令行输入：
yum install scim
yum install scim-pinyin
重启动X（按Ctrl+Alt+Backpace）或注销（logout）。
好了，可以输入中文了。CentOS系统出现中文乱码的问题就这样解决了。