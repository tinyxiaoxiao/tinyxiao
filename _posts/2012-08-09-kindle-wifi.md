---
layout: post
title: kindle4 wifi 连接电脑共享的wifi
categories:
- kindle
tags:
- tips
- kindle
---

kindle4 wifi 连接电脑共享的wifi

connectify 普通版不支持 宽频转换 
只能建立 adhoc网络 kindle 无法连接 


大家以前都在用的 Connectify PRO 3.5 
* Email  : dytoshare@student.undip.ac.id

* Serial :R67LZ2-6F4SFL-H99MHK-8DE821-1QT37X-1CSJ2S-B9ZXNG-5W4LE7-7FVE4U-W7BAE6-29C3BH-RV29KB-MJFW4M-Q37WR2-64BXBG-5K4RU3

or

* Email  : dytoshare@alumni.undip.ac.id

* Serial : DEC3SC-D8G8PS-3QLLMZ-DL9VA1-1QT3J3-1CSJ2S-B9ZXNG-5W4LE7-7FVE4U-W7BAEA-28C7NJ-FD64C3-7GRD2K-KBTFRV-DMEXLG-5GAPQ

大家都在用的这两个账户 已经不鞥用过期了，PRO最大的差別就是PRO可以宽频转换


Kindle 3的WIFI功能有一定限制，不是所有的无线网络都可以成功连接，官方文档里说了Kindle 3并不支持Ad-hoc或者peer-to-peer Wi-Fi网络，而我们常用的共享上网方法就是用windows自带的建立ad-hoc网络的功能，然后悲剧的是，Kindle不能成功连接。


为了让Kindle能够和笔记本电脑共享上网，只能使用第三方的工具了，还好有免费的Connectify软件，可以在这里下载：Connectify最新版下载
替代版：3.4 猛击此处

设置无线模式了，一定要选择WPA2，因为ad-hoc是Kindle不支持的。

win7系统自带 wifi 共享  设置方法\

以操作系统为win7的笔记本或装有无线网卡的台式机作为主机。 
主机设置如下： 

* 1、以管理员身份运行命令提示符： 
开始菜单-搜索cmd-右击以管理员方式运行 
* 2、启用并设定虚拟WiFi网卡： 
运行命令：netsh wlan set hostednetwork mode=allow ssid=wuminPC key=wuminWiFi
此命令有三个参数，mode：是否启用虚拟WiFi网卡，改为disallow则为禁用。 

1. ssid：无线网名称，最好用英文(以wuminPC为例)。 
2. key：无线网密码，八个以上字符(以wuminWiFi为例)。 
以上三个参数可以单独使用，例如只使用mode=disallow可以直接禁用虚拟Wifi网卡。 
开启成功后，网络连接中会多出一个网卡为“Microsoft Virtual WiFi Miniport Adapter”的无线连接2，为方便起见，将其重命名为虚拟WiFi。若没有，只需更新无线网卡驱动就OK了。 
* 3、设置Internet连接共享： 
在“网络连接”窗口中，右键单击已连接到Internet的网络连接，选择“属性”→“共享”，勾上“允许其他······连接(N)”并选择“虚拟WiFi”。 
确定之后，提供共享的网卡图标旁会出现“共享的”字样，表示“宽带连接”已共享至“虚拟WiFi”。 
* 4、开启无线网络：【（将start改为stop即可关闭该无线网，以后开机后要启用该无线网只需再次运行此命令即可） 
至此，虚拟WiFi的红叉叉消失，WiFi基站已组建好，主机设置完毕。笔记本、带WiFi模块的手机等子机搜索到无线网络wuminPC，输入密码wuminWiFi，就能共享上网啦！ 
附：显示无线网络信息命令：netsh wlan show hostednetwork 
虚拟无线AP发射的WLAN是802.11g标准，带宽为54Mbps。 


When it is run in "Access Point" mode, Connectify is a real WiFi Access Point running on your computer. Any device that can connect to a regular access point, can connect to a Connectify Hotspot, with no special setup or software required.

When Connectify is run in "Ad Hoc" mode it sets everything up for you (Wireless card, Internet sharing, firewall, etc.) in one press of a button. It also provides advanced features like showing you what computers are connected to your network, and letting you right click them to Explore their shared drives and printers.

NOTE: Users can purchase the PRO version of the application (includes features like Share Wi-Fi from 3G/4G Networks, Fully-customizable SSID, AutoInternet selection or Simple Firewall Controls) here.
