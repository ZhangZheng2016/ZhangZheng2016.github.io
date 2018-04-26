---
layout: post
title:  "高通毫米波网卡配置（4）"
date:   2016-11-30 19:52:25
categories: 网卡
tags: 高通 网卡 毫米波 60GHz
---

* content
{:toc}




# (五)	测试连接
## 1. ping测试
直接ping对方的IP地址
 
ubuntu和windows下一样。

## 2. iperf测试
Iperf 是一个网络性能测试工具。Iperf可以测试最大TCP和UDP带宽性能。Iperf具有多种参数和UDP特性，可以根据需要调整。Iperf可以报告带宽，延迟抖动和数据包丢失。接下来介绍iperf的安装。

[1]	windows（10）下iperf安装与使用
对于windows版的iperf，直接将解压出来的iperf.exe和cygwin1.dll放到系统路径当中。在文件内创建文件start.bat 内容是.\iperf3.exe –s
双击start.bat，即进入运行界面。
windows版本下iperf直接安装图形化GUI的Jperf。解压jperf-2.0.2.zip，运行jperf.bat
配置及结果如下图所示：
 
[2]	Ubuntu下iperf安装与使用
使用如下命令安装：

	 sudo apt-get update

	 sudo apt-get install iperf

#联网状态下使用这种方法，比较快捷

#未联网状态下可使用下列安装方法（所需gz包在配置文件中！）


	 gunzip -c iperf-.tar.gz | tar -xvf – 

	 cd iperf-3.0b5

	 ./configure 

	 make 

	 make install


server端（AP或者client都可以作为server端）:

	 iperf -s

client端：

	 iperf - -c 10.15.0.1 -P 1 -i 1 -p 5001 -f k -t 10

*******update*******
如果在client端，发送完之后，出现error，显示connection refused
考虑是两个PC网口设置的IP地址是够冲突。


Ubuntu下测试结果如图所示


[iperf](https://iperf.fr/iperf-doc.php)
网站中有iperf的使用说明。要注意的是，iperf在配置的时候客户端和host端是有区别的。测试过程未完待续...
基本测试到此结束。还有一些遮挡测试什么的，不重要了。
