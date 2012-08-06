---
layout: post
title: linux 服务器运维积累的几点
categories:
- linux
tags:
- Life
- linux
---

##linux 服务器运维积累的几点
###*nix查看文件目录大小
>du -sh 查看每个目录大小
当硬盘空间不够时，我们就很关心哪些目录或文件比较大
当前目录的大小：
du -sh .
当前目录下个文件或目录的大小：
du -sh *
显示前10个占用空间最大的文件或目录：
du -s * | sort -nr | head
-h已易读的格式显示指定目录或文件的大小
-s选项指定对于目录不详细显示每个子目录或文件的大小

###学会分析网站原始访问日志
>日志中记录了网站上所有资源的访问信息，包括图片、CSS、JS、FLASH、HTML、MP3等所有网页打开过程载入的资源，同时记录了这些资源都被谁访问了、用什么来访问以及访问的结果是什么等等，可以说原始访问日志记录了主机的所有资源使用情况。

###
>mysql-bin.000001、mysql-bin.000002等文件是数据库的操作日志，例如UPDATE一个表，或者DELETE一些数据，即使该语句没有匹配的数据，这个命令也会存储到日志文件中，还包括每个语句执行的时间，也会记录进去的。这主要是用于操作审查和多数据库同步的。ib_logfile则是用来记录InnoDB的表一致性的，只有在当机后才能发挥作用。

>1：数据恢复
如果你的数据库出问题了，而你之前有过备份，那么可以看日志文件，找出是哪个命令导致你的数据库出问题了，想办法挽回损失。
2：主从服务器之间同步数据
主服务器上所有的操作都在记录日志中，从服务器可以根据该日志来进行，以确保两个同步。

1：只有一个mysql服务器，那么可以简单的注释掉这个选项就行了。
vi /etc/my.cnf把里面的log-bin这一行注释掉，重启mysql服务即可。
2：如果你的环境是主从服务器，那么就需要做以下操作了。
A：在每个从属服务器上，使用SHOW SLAVE STATUS来检查它正在读取哪个日志。
B：使用SHOW MASTER LOGS获得主服务器上的一系列日志。
C：在所有的从属服务器中判定最早的日志，这个是目标日志，如果所有的从属服务器是更新的，就是清单上的最后一个日志。
D：清理所有的日志，但是不包括目标日志，因为从服务器还要跟它同步。
清理日志方法为：
PURGE MASTER LOGS TO 'mysql-bin.010';
PURGE MASTER LOGS BEFORE '2008-12-19 21:00:00';

如果你确定从服务器已经同步过了，跟主服务器一样了，那么可以直接RESET MASTER将这些文件删除。

##如何删除mysql-bin.0000X 日志文件呢?
]# /usr/local/mysql/bin/mysql -u root -p
Enter password:  (输入密码)
 />reset master; (清除日志文件)
]# du -h –max-depth=1 /usr/local/mysql/
再来查看下mysql文件夹占用多少空间?

]# find / -name my.cnf

找到了my.cnf 即mysql配置文件,我们将log-bin=mysql-bin 这条注释掉即可.

/# Replication Master Server (default)
/# binary logging is required for replication
/#log-bin=mysql-bin
重启下mysql吧.