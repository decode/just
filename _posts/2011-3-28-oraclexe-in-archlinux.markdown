---
layout: post
title: Install oracle-xe in archlinux
categories:
  - linux
---

由于某种需求,需要在linux下测试oracle服务器能否被局域网内的其它windows机器访问到,因此在机器上装了个oracle-xe 10g 体验版.

记录下安装过程,以免忘记.  

不能直接从aur源中安装oracle-xe,需要到oracle的官网上下载oracle-xe-univ-10.2.0.1-1.0.i386.rpm

到aur上找到oracle-xe.tar.gz的pkgbuild包解压,将上面的文件放到解压的文件夹里,PKGBUILD写得有点问题,要做一些修改  

> `find $startdir/pkg -type d -perm 700 -print0 | xargs -0 chmod 755`

修改为`find $startdir/pkg -type d -perm 700 -print0 | awk '{system("chmod 755 "$0)}' | awk '{system($0)}'`

然后运行makepkg,生成tar.xz后缀的文件,执行  

    sudo pacman -U oracle-xe-client-10.2.0.1-1-i686.pkg.tar.xz 

oracle-xe就安装到了系统了,安装完成后,会提示

    run \"/usr/lib/oracle/xe/app/oracle/product/10.2.0/server/config/scripts/oraconfig.sh\" to finalize your installation

照做就ok了

可能还要配置一下监听,才能正常访问:

    /usr/lib/oracle/xe/app/oracle/product/10.2.0/server/network/admin/listener.ora
  
    SID_LIST_LISTENER = 
    (SID_LIST = 
     (SID_DESC = 
      (SID_NAME = PLSExtProc) 
      (ORACLE_HOME = /usr/lib/oracle/xe/app/oracle/product/10.2.0/server) 
      (PROGRAM = extproc) 
     ) 
     (SID_DESC = 
      (GLOBAL_DBNAME = XE) 
      (ORACLE_HOME = /usr/lib/oracle/xe/app/oracle/product/10.2.0/server) 
      (SID_NAME = XE) 
     ) 
    ) 
    LISTENER = 
    (DESCRIPTION_LIST = 
     (DESCRIPTION = 
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC_FOR_XE)) 
      (ADDRESS = (PROTOCOL = TCP)(HOST = YOUR-HOST)(PORT = 1521)) 
     ) 
    ) 
    DEFAULT_SERVICE_LISTENER = (XE) 


配置参考： http://liangzhian0620.iteye.com/blog/705526
