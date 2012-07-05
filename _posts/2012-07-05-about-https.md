---
layout: post
title: HTTPS 详解
categories:
-Web development
tags:
- https
- SSL
---
##了解https 之前肯定要先了解http协议又名
- [Hypertext Transfer Protocol](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)


>由HTTP客户端发起一个请求，建立一个到服务器指定端口（默认是80端口）的TCP连接。HTTP服务器则在那个端口监听客户端发送过来的请求。一旦收到请求，服务器向客户端发回一个状态行，比如"HTTP/1.1 200 OK"，和响应的消息，消息的消息体可能是请求的文件、错误消息、或者其它一些信息。
HTTP使用TCP而不是UDP的原因在于打开一个网页必须传送很多数据，而TCP协议提供传输控制，按顺序组织数据，和错误纠正。具体细节请参考[TCP和UDP的不同](http://en.wikipedia.org/wiki/User_Datagram_Protocol#Comparison_of_UDP_and_TCP)
###通过HTTP或者HTTPS协议请求的资源由统一资源标识符（Uniform Resource Identifiers，URI）来标识。

## HTTP 是通过请求方法与服务器交互的：
- GET
>向特定的资源发出请求 ?id=3 
- POST  常用在提交表单；
>向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。
- PUT
>向指定资源位置上传其最新内容
- Delete
>请求服务器删除Request-URI所标识的资源。
- Trace
>回显服务器收到的请求，主要用于测试或诊断。
- Connect
>HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
- Head 
>向服务器索要与GET请求相一致的响应
- Options
>返回服务器针对特定资源所支持的HTTP请求方法。

##HTTPS 简介
HTTPS其实是有两部分组成：HTTP + SSL / TLS，也就是在HTTP上又加了一层处理加密信息的模块。服务端和客户端的信息传输都会通过TLS进行加密，所以传输的数据都是加密后的数据。具体是如何进行加密，解密，验证的，且看下图。
![https](http://blog.jobbole.com/wp-content/uploads/vb/1309-https.png)


