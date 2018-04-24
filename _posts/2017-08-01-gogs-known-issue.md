---
layout: post
title:  "Gogs已知问题"
date:   2017-08-01
tags: Gogs
---
1. 当仓库(repository)为公开时，无法用Eclipse的JGit插件push代码。Gogs bug为https://github.com/gogits/gogs/issues/4531，JGit的bug为https://bugs.eclipse.org/bugs/show_bug.cgi?id=513043，都未修复。临时解决方法为：改仓库可见性为私有。
1. 如果一个镜像一个仓库需要很长时间传输，镜像会失败（可能1小时超时）。
1. 还原备份文件时，即使文件不存在，也会查找attachement等文件。
1. 仓库(repository)和发布(release)的默认上传文件有限制，需要修改app.ini中，[repository.upload]下的FILE_MAX_SIZE或[release.attachment]下的MAX_SIZE。参考https://github.com/gogits/gogs/blob/master/conf/app.ini