---
layout: post
title:  "迁移SVN代码到git"
date:   2017-06-05
tags: SVN git
---
在已有代码需要向git迁移的时候，git官方提供的工具git svn可以方便的解决这个问题。
相关步骤如下：
1. 准备SVN人员名单
需要运行以下svn命令（需要Linux环境或者用Cygwin, msys2等Windows下的Linux环境）
```bash
svn log --username <SVN的用户名> <svn项目的url> -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2"@cloudwalk.cn>"}' | sort -u > users.txt
```
如果出现问题发生中断也不用担心，可以之后手工更新SVN人员名单。
1. 设定中文相关全局变量
```bash
# 设置文件名允许中文等字符
git config --global core.quotepath false
# 设置git界面编码
git config --global gui.encoding utf-8
# 设置git commit时的编码  
git config --global i18n.commitencoding utf-8
# 设置git log输出时编码  
git config --global i18n.logoutputencoding utf-8
export LESSCHARSET=utf-8
```
1. 在Gogs(或Gitlab, GitHub)上新建仓库(repository)
1. 初始化本地仓库
```bash
git svn init <svn项目的url>
```
1. 同步svn代码到本地仓库
```bash
git svn fetch --username <SVN的用户名> -A users.txt
```
其中的users.txt是第1步获得的SVN人员名单。
1. 添加远程仓库的url
```bash
git remote add origin <git仓库url>
```
其中的"git仓库url"是第3步创建的仓库的url。
1. 推送代码到远程仓库
```bash
git push origin master
```
如需推送到其他分支，则用以下命令
```bash
git push origin master:<远程分支名>
```

如果之后SVN有修改，仍需同步到git，则需进行如下操作
1. 继续同步svn代码
```bash
git svn fetch -A users.txt
```
1. 合并remotes/git-svn到本地的master分支
```bash
git merge remotes/git-svn
```
1. 推送代码到远程仓库(同之前的第7步)