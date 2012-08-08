---
layout: post
title: centos ip网关dns配置，ip网关不同网段上网方法
categories:
- linux
tags:
- tips
- linux
---

### Centos Linux 网络配置用到的一些方法备忘

###一、CentOS 修改IP地址
>修改对应网卡的IP地址的配置文件
vi /etc/sysconfig/network-scripts/ifcfg-eth0
修改以下内容
DEVICE=eth0 #描述网卡对应的设备别名，例如ifcfg-eth0的文件中它为eth0
BOOTPROTO=static #设置网卡获得ip地址的方式，可能的选项为static，dhcp或bootp，分别对应静态指定的 ip地址，通过dhcp协议获得的ip地址，通过bootp协议获得的ip地址
BROADCAST=192.168.0.255 #对应的子网广播地址
HWADDR=00:07:E9:05:E8:B4 #对应的网卡物理地址
IPADDR=12.168.1.2 #如果设置网卡获得 ip地址的方式为静态指定，此字段就指定了网卡对应的ip地址
IPV6INIT=no
IPV6_AUTOCONF=no
NETMASK=255.255.255.0 #网卡对应的网络掩码
NETWORK=192.168.1.0 #网卡对应的网络地址
ONBOOT=yes #系统启动时是否设置此网络接口，设置为yes时，系统启动时激活此设备
###二、CentOS 修改网关
>修改对应网卡的网关的配置文件
[root@centos]# vi /etc/sysconfig/network
修改以下内容
NETWORKING=yes(表示系统是否使用网络，一般设置为yes。如果设为no，则不能使用网络，而且很多系统服务程序将无法启动)
HOSTNAME=centos(设置本机的主机名，这里设置的主机名要和/etc/hosts中设置的主机名对应)
GATEWAY=192.168.1.1(设置本机连接的网关的IP地址。例如，网关为10.0.0.2)

###三、CentOS 修改DNS
>修改对应网卡的DNS的配置文件
 vi /etc/resolv.conf
修改以下内容
nameserver 8.8.8.8 #google域名服务器
nameserver 8.8.4.4 #google域名服务器

###四、重新启动网络配置
 >service network restart
或
 /etc/init.d/network restart
修改 IP 地址
即时生效:
 ifconfig eth0 192.168.0.2 netmask 255.255.255.0
启动生效:
修改 /etc/sysconfig/network-scripts/ifcfg-eth0
修改网关 Default Gateway
即时生效:
 route add default gw 192.168.0.1 dev eth0
启动生效:


### 配置过程中出现的以下问题及解决方法:  
>执行route add default gw 192.168.0.1 dev eth0
返回：SIOCADDRT: No such process

原因:ip与gateway不在一个网段内

那么 ip地址和网关不在同一个网段，Linux如何上网！

比如实验室网络就是这么怪，而且还是 mac地址绑定。
IP地址是 58.*.*.*
netmask是255.255.255.0
但是网关是 202.*.*.*
两者不在同一网段，以前配置虚拟机vmware 不少在这地方花时间！！！！！！
终于找到了解决的方法：

**先将网关IP当成一个主机加进来，这样在这两个IP直接建立一个连接,并且不设置掩码，即能到达所有其他网段。**
route add -host 202.194.20.254 netmask 0.0.0.0 dev eth0 

**然后再将网关IP加成网关**
route add default gw 202.194.20.254 netmask 0.0.0.0 dev eth0
可以添加到 开机启动项内 .vim /etc/rc.local

每次都能自动配置。 

