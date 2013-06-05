---
layout: post
title: diahosting服务器安装配置
categories:
  - linux
  - server
---

* reinstall os
  第一歩就是把原装的centos换成ubuntu10.04,需要几分鈡的时间

* 安装软件及环境
  > timezone

    dpkg-reconfigure tzdata

  > git

  > postgresql
    Create the file /etc/apt/sources.list.d/pgdg.list, and add a line for the repository:

      deb http://apt.postgresql.org/pub/repos/apt/ lucid-pgdg main

    Import the repository signing key, and update the package lists:

      wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
      sudo apt-key add -
      sudo apt-get update 

    参考: http://www.postgresql.org/download/linux/ubuntu/

    修改默认的用户密码: ALTER USER postgres with encrypted password 'your_password';

    参考: https://help.ubuntu.com/10.04/serverguide/postgresql.html
    
    修改默认的数据库编码:
    参考: https://wiki.archlinux.org/index.php/Postgresql

  > rvm
    curl -L https://get.rvm.io | bash -s stable --autolibs=enabled
    To start using RVM you need to run `source /usr/local/rvm/scripts/rvm`

    参考: https://github.com/wayneeseguin/rvm
