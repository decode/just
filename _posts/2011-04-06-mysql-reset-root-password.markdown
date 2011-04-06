---
layout: post
title: MySQL root密码重置
categories:
  - linux
---

好久没用mysql了,密码也忘却在风中,网上找了找如何恢复的方法,现在总结一下

* 重装
  
  ...

* 重置root密码

  首先停止mysql后台服务,然后执行下面的命令:

    mysqld_safe --skip-grant-tables
    mysql -u root

    mysql>use mysql

    mysql>update user set password=password("new-password") where user="root";

    mysql>flush privileges;

    mysql>exit

  解决问题

END
