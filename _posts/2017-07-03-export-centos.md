---
layout: post
title:  "临时导出无法启动的CentOS系统中的文件"
date:   2017-07-03 11:51:38 +0800
categories: jekyll update
---
前些天发现a.b.c.d服务器无法启动，开机报如下错误
{% highlight shell %}
Attempting Boot From Hard Drive (C:)
.
error: file '/grub2/i386-pc/normal.mod' not found
grub rescue> ls
(hd0) (hd0,msdos2) (hd0,msdos1) (hd1) (hd2) (hd3) (hd4) (hd5) (hd6) (hd7) (hd8)
(hd9) (hd10) (hd11) (hd12) (hd13) (hd14) (hd15)
grub rescue> _
{% endhighlight %}

按照网上教程，用光盘启动修复安装grub无效，但可以访问之前的文件系统，进而恢复文件系统。大致步骤如下

* 从CentOS光盘启动后，选择rescue mode
* 一路默认选择，直到提示原有文件系统将会挂载到/mnt/sysimage
* 由于原文件系统中的/bin目录下的文件被清空，无法chroot到/mnt/sysimage
* 检查/mnt/sysimage/home/public，发现之前容器中保存的数据还在
* tar命令在光盘系统中没有，但可以zip打包：zip -r public.zip public
* 挂载移动硬盘，但文件系统是ntfs，在光盘系统中不支持
* 考虑用网络传输，但rescue mode下没有IP，需要设置：ifconfig eno1 a.b.c.d
* 光盘系统中有python，于是架设简单文件服务器：python -m SimpleHTTPServer 8000
* 在另一台机器上，curl a.b.c.d:8000，返回如下
{% highlight html %}
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 3.2 Final//EN"><html>
<title>Directory listing for /</title>
<body>
<h2>Directory listing for /</h2>
<hr>
<ul>
<li><a href="backup/">backup/</a>
<li><a href="backup_96_jenkins/">backup_96_jenkins/</a>
<li><a href="cld/">cld/</a>
<li><a href="data/">data/</a>
<li><a href="dockerfiles/">dockerfiles/</a>
<li><a href="fullbackup/">fullbackup/</a>
<li><a href="lib/">lib/</a>
<li><a href="oracle-instantclient11.2-basic-11.2.0.4.0-1.x86_64.rpm">oracle-instantclient11.2-basic-11.2.0.4.0-1.x86_64.rpm</a>
<li><a href="oracle-instantclient11.2-sqlplus-11.2.0.4.0-1.x86_64.rpm">oracle-instantclient11.2-sqlplus-11.2.0.4.0-1.x86_64.rpm</a>
<li><a href="oracle11_install_new.tar">oracle11_install_new.tar</a>
<li><a href="public/">public/</a>
<li><a href="public.zip">public.zip</a>
<li><a href="test/">test/</a>
<li><a href="tmp/">tmp/</a>
<li><a href="yc/">yc/</a>
<li><a href="zabbix/">zabbix/</a>
</ul>
<hr>
</body>
</html>
{% endhighlight %}
* 用wget下载之前打包的public.zip: wget a.b.c.d:8000/public.zip
