---
layout: post
title: Archlinux一些安装配置拾遗
categories:
  - linux
---

最近又装了archlinxu到几台笔记本上，为了以后难免会忘记，记录下一些小细节。

* Toshiba笔记本亮度不能自动调节，每次重启都会回到最高亮度的问题：

  在/etc/profile里加上："echo 3 > /sys/class/backlight/acpi_video0/brightness"

  数字表示需要的亮度值
  

* GDM中自动启用fcitx输入法

  可以在~/.profile中加入以下代码：

  export XMODIFIERS="@im=fcitx"
  export GTK_IM_MODULE=xim
  export QT_IM_MODULE=xim
  killall fcitx
  fcitx &

  从目前使用情况来看，暂时没有什么问题。

* gnome-shell的小插件

  gnome-shell-system-monitor-applet-git: 在状态栏上显示cpu、mem、swap、net的情况，不错的指示器

  gnome-shell-theme-gaia: 一个清爽的主题

  gnome-tweak-tool: 一个配置gnome-shell的工具，包括桌面、字体、shell主题、shell插件等等，如果使用gnome-shell必装

* 按键映射

  Toshiba的笔记本键盘进水了，吹风机风干以后，空格键就废了，只能想办法将别的键替换了，网上找了找资料，用xmodmap就能解决问题。

  首先看看自己系统上有没有xmodmap这个命令，如果没有，老实输入yaourt xorg-xmodmap装上。还有xev，一个输出X事件的工具，没有也用yaourt xorg-xev。
  
  然后用xev，看自己的需要替换的按键代码(keycode)，我准备把它映射到右alt键，主要是这个键我不太常用。在我的机器上右alt的keycode是108。执行下面的代码就行了：

  xmodmap -e "keycode 108 = space"
  
  要把它映射成空格键，每次启动的时候都自动加载，就将这段代码加到~/.profile里面去。


更多问题，求助https://wiki.archlinux.org/index.php/Main_Page, 里面会有答案。

END
