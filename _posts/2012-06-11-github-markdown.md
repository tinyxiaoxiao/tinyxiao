---
layout: post
title: 第一篇文章github+markdown构建博客
categories:
- tools
tags:
- github	
- markdown
---


# 第一篇 github+markdown构建博客

1.markdown 语法参看教程 [markdown](http://wowubuntu.com/markdown/index.html)
2.github 简介：
>git 一个强大的版本管理工具。

git 全局设置：
`git config --global user.name "Your Name"
git config --global user.email youremail@email.com`


##**将Ｇit项目与Github建立联系**
`mkdir yourgithubproject
cd yourgithubproject
git init
touch README
git add README
git commit -m 'first commit'
git remote add origin git@github.com:yourgithubname/yourgithubproject.git
git push origin master`

##**导入现有的Git仓库**
`cd existing_git_repo
git remote add origin git@github.com:yourgithubname/yourgithubproject.git
git push origin master`

[pandoc](http://code.google.com/p/pandoc/) 强大的文档转换工具，极客必备杀器，以防愣头客户索要Word版本


##how to create a jekyll blog? 简易搭建github博客系统
[官方教程The Quickest Way to Blog with Jekyll](http://jekyllbootstrap.com/)
###1. step1 ： 注册 [github](http://github.com)
> easy to register? ok ? yep!

###2. step2： 配置 [github configuration ](https://help.github.com/articles/set-up-git#platform-windows)

>注册完成以后需要做的是配置github ：
1.安装git[download](http://git-scm.com/downloads)
2.配置git
打开 git Bash; 全局配置如下：

###3. step3：  建立一个新的github repository 
>比如我的帐号 tinyxiaoxiao 那就建立一个名字tinyxiaoxiao.github.com 的 repository

###4.step4： install jekyll-bootstrap-Core
`$ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com
$ cd USERNAME.github.com
$ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git
$ git push origin master`

###5.step5：now 你就可以访问你的主页了 USERAME.github.com  [me](tinyxiaoxiao.github.com)


