---
layout: post
title: 	轻量级写作之瑞士军刀pandoc
categories:
- tools
tags:
- pandoc
- markdown
- html5
---
###轻量级文档写作：
>日常任务重经常的时间浪费在 调格式word wps 等个版本之间的兼容性上。
>直到遇到了markdown标记性语言,后顿时眼前一亮.
简洁的语法简直让人爱不释手 

[markdown教程](http://wowubuntu.com/markdown/index.html)

###常用的文件查看方式
- 邮件
- 打印
- PDF
- 网页
- PPT 
**如何让编辑一次的文字 在所有查看方式中通用呢？**

>markdown 恰恰能做到！

>Markdown是这里要介绍的第一个轻量级标记语言。
它面向表现，所见即所得。
它非常简单，以至于简单到简陋的程度。
其作者John Gruber是一个狂热果粉，不难想象他对这个语言简约程度的强迫症程度。

##用Pandoc处理Markdown 
[pandoc](http://johnmacfarlane.net/pandoc/)文档处理的瑞士军刀

>比较常见的演示手段是用LaTeX Beamer生成若干幻灯片，然后用PDF阅读器全屏播放。


Pandoc可以将Markdown转换成Slidy和S5（HTML代码），然后用网页浏览器来播放。

[Slidy](http://www.w3.org/Talks/Tools/)是W3C推荐的。跟PDF幻灯片唯一的区别是，讲义需要另外生成的。

##[pandoc](http://johnmacfarlane.net/pandoc/)文字处理瑞士军刀

如果你需要把文件从一种标记语言格式转换到另一种格式，pandoc会是你的瑞士军刀。它可以把markdown、 reStructuredText、 textile、 HTML、或者LaTeX转换成：

`HTML格式: XHTML, HTML5, 以及HTML幻灯片Slidy， S5，或者DZSlides.
文字处理软件格式： Microsoft Word docx, OpenOffice/LibreOffice ODT, OpenDocument XML
电子书： EPUB
文档格式： DocBook, GNU TexInfo, Groff man pages
TeX格式： LaTeX, ConTeXt, LaTeX Beamer slides
PDF via LaTeX
轻量级标记语言格式： Markdown, reStructuredText, AsciiDoc, MediaWiki markup, Emacs Org-Mode, Textile`

### [如何安装pandoc](http://johnmacfarlane.net/pandoc/installing.html) [在线使用](http://johnmacfarlane.net/pandoc/try)
####[download here](http://code.google.com/p/pandoc/downloads/detail?name=pandoc-1.9.4.2-setup.exe&can=2&q=)
##[demo](http://johnmacfarlane.net/pandoc/demos.html)

>HTML slide shows:
pandoc -s --mathml -i -t dzslides SLIDES -o example16a.html
pandoc -s --webtex -i -t slidy SLIDES -o example16b.html
pandoc -s --self-contained --webtex -i -t s5 SLIDES -o example16c.html
pandoc -s --self-contained --mathjax -i -t slideous SLIDES -o example16d.html

##制作幻灯片工具
 
[landslide  markdown ](https://github.com/adamzap)landslide
 
[sozi svg](http://sozi.baierouge.fr/wiki/en:welcome)
 
[impress.js](http://bartaz.github.com/impress.js)
 
[prezi flash   ]( http://prezi.com/)



