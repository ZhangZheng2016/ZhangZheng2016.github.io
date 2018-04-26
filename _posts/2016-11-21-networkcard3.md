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

配置地址之后就能实现的原因可能是网卡对地址的处理不善。（对DHCP协议执行不力）
需要人工配置IP地址的问题已经解决，是因为原来在initAP中设置的IP地址并不是在dhcp.conf中设定的网段。（10.0.0.1才行）