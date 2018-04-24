---
layout: post
title:  "Jenkins无法收到邮件(Not sending mail to unregistered user)"
date:   2017-05-24
tags: Jenkins email
---
在Editable Email Notification中配置了Triggers->Always，但是总是收不到邮件。在控制台中发现如下记录

Not sending mail to unregistered user abc@def.ghi

**原因**：

未设置密码的用户所关联的email被认为未注册。

**解决方法**：

在Jenkins->系统管理->管理用户中找到未注册的用户，选择"设置"，设置密码。
