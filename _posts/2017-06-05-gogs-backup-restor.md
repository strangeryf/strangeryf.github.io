---
layout: post
title:  "Gogs的备份与还原"
date:   2017-06-05
tags: Gogs
---
本文涉及到的操作为Gogs提供的backup和restore两个命令。如在一台机器上需要导入另一台机器上的数据，则两台机器的环境要保持一致，即
* Windows x64
* Gogs 0.11.4.0405 x64
* MySQL 6.3 x64
* 目录结构相似（比如都有D盘）
同一台机器的备份还原步骤类似。

在用户使用较少的时间段，在主Gogs机的Gogs安装目录执行命令
```shell
D:\gogs>gogs backup
2017/06/05 13:30:10 [ INFO] Backup root directory: C:\Users\jerry\AppData\Local\
Temp\2\gogs-backup-726324151
2017/06/05 13:30:10 [ INFO] Packing backup files to: gogs-backup-1496640610.zip
2017/06/05 13:30:10 [ INFO] Dumping repositories in 'D:/gitrepo'
2017/06/05 13:32:51 [ INFO] Repositories dumped to: C:\Users\jerry\AppData\Local
\Temp\2\gogs-backup-726324151/repositories.zip
2017/06/05 13:35:26 [ INFO] Backup succeed! Archive is located at: gogs-backup-1
496640610.zip
```
在备用Gogs机上(须安装好MySQL, Gogs)
1. 复制主Gogs上的配置文件（Gogs安装目录\custom\conf\app.ini）到备用Gogs机的Gogs安装目录
1. 复制主Gogs机上的备份文件到备份机的Gogs安装目录
1. 如果两边的数据库用户名、密码不一致，需要修改该配置文件与备用机的数据库一致
1. 如果没有repository的ROOT属性指定的路径，则创建该目录
1. 修改server的ROOT_URL属性为备用机的IP
1. Gogs目录下，如有custom.bak， data\avatar.bak目录，则删除该目录
1. 在Gogs安装目录执行以下命令
```bash
gogs restore --from <主Gogs上的备份文件> --config app.ini -t <与安装目录同一盘符的临时文件夹> -v
```
1. 如果报错说无法移动xxx\data\attachment，则须在临时目录创建data\attachment目录，再次运行上述命令。如果有其他报错，需要删除，或建立相应的文件夹。
1. 还原完成之后，打开配置文件（Gogs安装目录\custom\conf\app.ini），修改其中的目录、IP等与备份机不一致的部分。之后，运行gogs web命令启动Gogs。
 