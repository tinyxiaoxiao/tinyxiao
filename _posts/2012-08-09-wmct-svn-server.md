---
layout: post
title: WMCT 实验室 SVN 服务器使用指南
categories:
- linux
tags:
- tips
- svn
---

###WMCT 实验室 SVN 服务器使用指南


>####windows用户安装项目组群共享的tortiseSVN 或[点击下载](http://dl.pconline.com.cn/download/53122.html)[](http://tortoisesvn.net/downloads.html)
   * linux 用户 相应版本，自行搜索下载[RabbitVCS](http://www.rabbitvcs.org/ )有
   * mac 也有相应版本，自行搜索下载 [Versions - Mac Subversion Client SVN](http://versionsapp.com)

>####2. WMCT代码仓库 介绍 
    地址:svn://58.194.170.76/

---
* svn://58.194.170.76/wmct-dev 终端组代码仓库
* svn://58.194.170.76/wmct-cloud云计算组代码仓库
* svn://58.194.170.76/wmct-iot 物联网组代码仓库
* svn://58.194.170.76/wmct-public WMCT公共仓库
暂未开启http服务，只支持svn访问方式
---
>登录账户：实验室每个人都有一个账户密码
形式为： 比如  张三 用户名:zs 密码:******
各个人分属不同组有不同仓库的权限：

* 1).全部具有 公共仓库权限

* 2).终端组 只具有 wmct-dev 权限和 public 权限

* 3).云计算 只具有 wmct-cloud 权限和 public 权限

* 4).之后就可以备份你的工程，eclipse 有相应插件 可以 设置 同步你的代码 永不丢失。

* 你的每一次commit 都有记录,随时revert it

* 同时支持多人协作。还有更多新的功能，与您共享~

####3.公共FTP  [ftp://58.194.170.76](ftp://58.194.170.76)
 