---
layout: post
title: 在Diahosting Ubuntu中配置邮件服务
categories:
  - linux
---

换了服务器之后,系统的邮件发送服务一直处于半瘫痪状态,今天终于狠下心,抽了个时间解决掉这个缺陷.

题外话:服务器用的是Diahoting的ubuntu 9.10系统,很多软件都比较老,一开始配置passenger就费了老大的劲头,之后再也不想去碰了.每次配置都是一次痛苦的体验,还是比不上archlinx的便利性.不过好在服务器比较稳定,配置好之后也省了不少的心

这个系统用的是exim4的邮件服务,默认是无法往外发送邮件的.需要重新配置:

  > dpkg-reconfigure exim4-config

在显示的对话框中选择第一条internet site,system mail name服务器的名字之类的一律填注册的域名或ip地址,一路默认基本就没有问题了.

测试是否成功:

> echo foo | exim -d your@mail_address

END
