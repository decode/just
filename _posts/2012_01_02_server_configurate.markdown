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

END
