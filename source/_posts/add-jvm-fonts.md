title: 解决geoserver中文label乱码问题
date: 2016-03-07 16:26:36
category: gis
tags:
---
将geoserver部署到ubuntu的时候，遇到label显示中文乱码的问题，记录下解决过程：

进入j2sdk目录，比如/usr/lib/jvm/java-7-openjdk-amd64/jre/lib，创建fallback目录：

    sudo mkdir fonts/fallback

拷贝字体文件到fallback目录

    cp xxx.ttf /usr/lib/jvm/java-7-openjdk-amd64/jre/lib/fonts/fallback
安装fontconfig

    sudo apt-get install fontconfig
rebuid fonts caches

    fc-cache –fv
    
restart JVM