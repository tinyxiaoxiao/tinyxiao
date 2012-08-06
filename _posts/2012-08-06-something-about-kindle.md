---
layout: post
tile: kindle4 你必须知道的那些事
categories:
- kindle
tags:
- my life
- kindle
---

###kindle4 你必须知道的那些事

####前言: 纠结了很长时间的kindle4 终于到手了，图就不放了。到手这么长时间了也做个总结。
>购买过程:正好赶上活动 kindle4官翻广告版49刀拿下，可现在amazon为了推出他新版kindle现在正进行40%的折扣活动，着实心里一惊，上网一看:

>Amazon.com：现有部分Kindle及所有Kindle 配件40% OFF优惠！结账时输入优惠码 KINDLE40，需要使用您的Amazon.com Rewards Visa 卡结账

*可惜天朝用户:无法申领 信用卡啊····*

1.淘宝 卖家代下单49刀 汇率6.3 共计315 元
2.转运公司 第一次海购没经验选了个垃圾的转运中国。具体怎么垃圾我在开帖祥述.
3.我心疼的小k在海关带了一个月 才出来 交了 88元的税。
4.最后 ems到手
一句话 : 在天朝就是难···

购买过程写完了，接下来到了兴奋的时刻，总结一下kindle的用法；

1.注册 网上 很多注册的 帖子需要注意的是美国的地址，我也顺着用哈佛的地址注册了一下。
为什么要注册捏? 
>首先不注册没法看书。
其次注册后你会发现真的很强大很便利。
亚马逊网上就可以管理你的kindle。 

RSS阅读每天发送你订阅的博客到你的kindle，从此摆脱电脑。

精选了如下服务和应用。

对于一个阅读狂:Google Reader 绝对是不可缺啥的。
提供RSS 订阅的网站：
1.狗耳朵: www.Dogear.mobi 这个网站的服务成立有一段时间了，最近还把服务托管到www.whycai.com上，想必有更好的硬件资源。该服务网站可以订阅推送许多热门的中外新闻和博客内容，比如纽约时报，The BBC等。Dogear甚至宣称可以将Google Reader的内容推送到Kindle。不过，即使是常见的中外新闻和博客已经能满足大多数人的需求了。

更为优秀是此网站提供自主添加RSS内容功能，即用户如果找不到自己需要的内容，可以自行将需要的网站RSS源添加到网站

狗耳朵 最近打不开了。服务器到期了

2. 爱看豆( http://ikandou.com )  ：只允许两个订阅 显然太少 不够用了。
3.Kindlefeeder: www.kindlefeeder.com 这个国外网站可以订阅许多新闻网站的内容，

4.kindle4rss 这个 做得很不错，提供图片支持。堪称完美。但是美中不足的是只支持 12个订阅，再多就要付费了，很便宜每天只要两毛钱。

5. http://www.klip.me/ 和 chrome的send to kindle的插件可以将网页发送到kindle上。

最后介绍的对于一个技术狂来说的[开源工具]
[kindlereader](https://github.com/jiedan/kindlereader)     不想折腾的 可以 试试        [开源实例](http://gr2k.rockywang.info)

###17种Kindle用户必备的软件工具
Kindle用户要在茫茫资源海中找到真正实用的工具并非易事，这篇文章就为你收集了17个Kindle必备软件，从电子书格式转换到网页投递，只有你想不到，没有它做不到。

这些软件中有许多不是专门为Kindle开发的，如果你使用的是其他电子阅读设备，一样会发现它们非常有用，比如PDF页面裁剪，电子书格式转换，等等。

软件分类包括：阅读工具，通用格式转换工具，PDF优化工具，Kindle文件管理工具和网页投递工具。

阅读工具：

1. Kindle云阅读: 走到哪读到哪
2. Kindle Reader for PC and Mac: 在电脑上看电子书

3. Kindle Previewer: 预览转换后的电子书在Kindle上的版式

 通用格式转换工具：
4. 亚马逊Kindle邮件转换服务: 免费的在线转换服务

5. Calibre: 电子书转换和管理

6. Hamster Free eBook Converter: 轻便但强大的电子书转换工具

7. Auto Kindle eBook Converter: 将PDF, Lit, and HTML 格式文件转为MOBI 格式

PDF优化工具：

8. Briss: 可视化PDF页面调整工具

9. K2PDFopt: 将版式复杂的PDF文件变的易于在Kindle上阅读

Kindle文件管理工具： 


10. Koll3ction: 使用文件夹结构来管理你的Kindle文件

网页投递工具：

11. SENDtoREADER: 书签工具，发送任意网页和Google Reader中的内容到你的Kindle

12. Kindle It: 浏览器扩展，发送网页到Kindle

13. KindleFeeder: 通过whispernet（亚马逊3G网络服务，收费）投递最多12条RSS订阅到Kindle

14. Greader2Kindle: 在Kindle上看Google Reader订阅内容

15. Instapaper:自动投递Instapaper中未阅读的文章到Kindle

16. ReadItLater: 自动投递ReadItLater中未阅读的文章到Kindle

17. Readability:自动投递Readability的阅读清单到Kindle

其他工具：一看就会用，不用写简介了


###原理简述：利用搭建在gae上的kindlereader读取网络rss链接，经程序自动内容整合，定时投递到zephyrxtcom@free.kindle.com由Amazon提供的免费转换帐号，最后就可以在kindle上用wifi自动接收到已经排版定制好的”rss书籍”。虽然搭建过程显得比较复杂，但是一劳永逸，值得一试！

注：kindlereader(https://github.com/jiedan/kindlereader由dogear站长友情开源分享)

以下说明以目前最新版本kindlereader 0.3.3为例，如果搭建期间遇到“网络故障”，可以使用预备的跨栏手段解决；

前期准备：

1.一台可以上网的电脑
2.一台已经激活的正常工作的kindle3（WIFI&3G）——kindle3使用参考指南
3.一个gae帐号（注册地址：https://appengine.google.com/ ）
4.一个可以用来接受gae帐号激活信息的移动手机
5.一些跨栏的手段（避免可能随时遇到的“重置”网络故障）
6.一个域名（注册参考：http://zephyrxt.com/archives/7207）
域名用来绑定gae程序
作用：将原本zephyrxtcom.appspot.com绑定为mykindle.mydomain.com这样的形式，减轻因appspot.com在中国大陆无法访问造成的使用麻烦，

帐号注册指南：

1.gae：
使用gmail帐号登录注册：https://appengine.google.com/ ，点击“create application”，进入到帐号短信激活界面，选择others
，使用8613800138000这样的号码（注：86为中国国家代码），输入完毕点击send，稍后就可以在手机上收到激活信息；成功注册后，就可创建属于自己的gae程序了（一个GAE帐号有10个免费限额）
待激活后再次点击create application，在Application Identifier一栏输入所心仪的名称，例如，zephyrxtcomkindle（如果已被他人注册，需要重新选择！）。其余选项保持默认即可，点击页尾的Create Application即成功创建了一个gae程序（用来上传kinldereader之用）。

kindlereader上传完毕后即可用zephyrxtcomkindle.appspot.com这样的网址访问使用。上传方法见下文；
2.域名注册指南：http://zephyrxt.com/archives/7207 此文已有详细的说明。
域名绑定google企业套件参照官方说明：http://www.google.com/apps/intl/zh-CN/business/index.html

软件工具准备：

1.下载kindlereader最新的GAE源程序，进入到
https://github.com/jiedan/kindlereader/tree/gae 点击“ZIP”下载源码，然后解压
2.App Engine SDK（上传kindlereader到gae之用）：
http://code.google.com/intl/zh-CN/appengine/downloads.html 下载http://googleappengine.googlecode.com/files/GoogleAppEngine-1.5.3.msi 默认安装即可（视情况而定可能还需安装python平台，依提示操作即可）

配置程序及上传
kindlereader配置说明：

安装
修改 app.yaml 中 application id, #以文中为例，此处修改成zephyrxtcomkindle
将 config.example.py 更名为 config.py 并配置其中内容
如果账单开启则将 queue.example.billing.yaml 更名为 queue.yaml 否则将 queue.example.yaml 更名为 queue.yaml #选择后者
使用 Google App Engine Launcher 上传至服务器
config.py 详细说明：

/# coding=utf-8

/# ‘id’.appspot.com or custom domain
base_domain = “zephyrxtcomkindle.mydomain.com” #此处修改成欲绑定的域名

/# Email address of the sender
/# The address of a registered administrator for the application. You can add administrators to an application using the Administration Console(http://code.google.com/appengine/docs/adminconsole/index.html).
/# more info http://code.google.com/intl/zh-CN/appengine/docs/python/mail/sendingmail.html
mail_sender = example@gmail.com #此处修改成登录所用的google帐号即可

/# Google OAuth info
/# Get it from https://www.google.com/accounts/ManageDomains
consumer_key = “XXXXXXXXXXX”
consumer_secret = “XXXXXXXXXXX” #以上两栏需要登录以上网址生产

/# Billing Status (True or False)
billing_enabled = False
”

配置完成后就可以正式上传
详细步骤：复制已经修改配置完毕的kindlereader文件夹到App Engine SDK安装目录。开始-运行-输入CMD，进入到App Engine SDK安装目录；例如：cd C:\\google\sdk
再输入“上传”命令：appcfg.py update kindlereader ，依次输入Email帐号及帐号密码（密码输入时屏幕不显示）既可成功上传。

完毕后，就可登录zephyrkindle.appspot.com查看效果了（如果无法登录，记住跨栏）

搭建最后一步，绑定域名

回到https://appengine.google.com/ 点击进入zephyrxtcomkinle，在Adminstration-Applicationg settings-Domain setup，输入之前已经注册好了的域名“mydomain.com”，按提示操作即可顺利绑定.

成功后就可使用zephyrxtcomkind.mydomin.com这样的个性网址访问使用kindlereader了！

测试验证：
登录reader.google.com，加入rss订阅，在zephyrxtcomkindle.mydomain.com适当设置及授权，保持设置后“测试投递”如kindle3在wifi联网的情况下成功接收！表示搭建正式完毕！

一些必要的操作.将sender的Email帐号加入到Amazon的approve list列表中（否则无法转换） 、
END by Zephyrxt.com  

