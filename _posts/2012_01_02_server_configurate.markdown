---
layout: post
title: 服务器安装配置拾遗
categories:
  - linux
---

* 添加用户

  > useradd -G users,wheel -m username
  > passwd username

* passenger安装配置

  > gem install passenger
  > passenger-install-nginx-module

  会遇到提示有必要的系统软件没有安装
  > yaourt gcc pkg-config libcurl3 imagemagick
  如果是64位系统，安装libcurl3时会提示系统架构不支持64位，这是因为packagebuild文件里arch=i686，改成arch=x86\_64就可以成功编译了。

* mysql安装配置

  > mysqladmin -u root password xxx

  给用户权限 grant all privileges on database.* to user@localhost identified by "password";

  数据库备份导入
  > mysql -u root -p database_name < backup.sql

* 安装邮件服务

  > yaourt postfix

* rails 部署中的问题

  1. capistrano

    如果是新的服务器环境，在本机当前项目目录下，运行cap deploy:setup

    运行cap deploy
  
  2. passenger出错，摘要如下：

    uninitialized constant Compass::Logger (NameError)
    compass/version.rb 56 in `const_missing'

    解决方法：

    lib/compass.rb:
    -%w(dependencies util browser_support sass_extensions version errors quick_cache).each do |lib|
    +%w(dependencies util browser_support sass_extensions version errors quick_cache logger).each do |lib|
    
    参考：https://github.com/chriseppstein/compass/issues/438

* 自动备份

  > gem install astrails-safe

update:

* 解决linode下使用pacman更新系统发生的问题

  error: failed to commit transaction (conflicting files)
  filesystem: /etc/mtab exists in filesystem
  Errors occurred, no packages were upgraded.

  输入:
    pacman -S filesystem --force

update 2:

* ubuntu8.04下的一些配置

  bundle install下mysql gem出错
  尝试解决: aptitude install libmysqlclient16-dev

  rmagick gem安装出错
  下载imagemagick源代码,编译

  sqlite3 gem安装出错
  下载源代码编译

  crontab修改默认editor
  在.bashrc里加入 export EDITOR=vim

  passenger无法找到bundle install后的gems
  运行 bundle --deployment

END
