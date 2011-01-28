---
layout: post
title: Vsftpd short howto
categories:
  - linux
---

为了能让wordpress在线升级，需要一个ftp服务器，以便wordpress能够具有服务器的写权限。翻来翻去，找到了这个vsftpd，只需要在服务中启用vsftpd，在wordpress里升级的时候填好用户名和密码就轻松的升级到最新的版本了。

另外启用了vsftpd以后，使用本地用户登录之后，所有的文件都在登录用户的家目录中。

/etc/vsftpd.conf的一些设置：

1. 限制匿名用户访问ftp：
anonymous_enable=NO

2. 解决使用本地用户登录ftp后可能出现的访问系統文件的问题：

 `` chroot_local_user=NO ``

 `` chroot_list_enable=YES ``

 `` chroot_list_file=/etc/vsftpd.chroot_list ``

在vsftpd.chroot_list文件中添加要限制的用户名，在这名单里的用户就会被限制在家目录里了。

> vsftp offical website: http://vsftpd.beasts.org

> 配置参考：http://www.brennan.id.au/14-FTP_Server.html
