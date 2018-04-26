---
layout: post
title:  "高通毫米波网卡配置（3）"
date:   2016-11-21 00:08:50
categories: 网卡
tags: 高通 网卡 毫米波 60GHz
---

* content
{:toc}



## Ubuntu下的连接
开启AP模式之后就能在另一台ubuntu电脑（也安装该网卡）上搜索到该AP了，按照如下配置
![ubuntupeizhi](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/001.png)

配置地址之后就能实现的原因可能是网卡对地址的处理不善。（对DHCP协议执行不力）
需要人工配置IP地址的问题已经解决，是因为原来在initAP中设置的IP地址并不是在dhcp.conf中设定的网段。（10.0.0.1才行）

## windows（10）下的连接
~~在windows下无法搜索到该AP，原因未知，问题待解决。猜测是windows对天线硬件不支持。~~
widows无法搜索到AP问题已解决。由于中间对AP电脑配置进行过多次改动，暂不清楚具体缘由。猜测是将AP从80211的channel1改动到了channel2的原因。

![win10](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/002.png)

在连接到AP之后还需要配置一下，配置详情见下图：

![peizhi](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/003.png)

在配置之后，就能ping通了。
