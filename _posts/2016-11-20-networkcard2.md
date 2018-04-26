---
layout: post
title:  "高通毫米波网卡配置（2）"
date:   2016-11-20 00:06:05
categories: 网卡
tags: 高通 网卡 毫米波 60GHz
---

* content
{:toc}




# (四)	连接问题
## 配置AP
我们在初期测试网卡时，需要用到hostapd将其中的一个网卡配置成AP模式，接下来是hostapd的配置过程。

*以下均是在ubuntu的root权限之下的终端操作
*root权限也不是万能的，也需要对文件、文件夹进行权限修改

	 iwconfig
#此时显示的是网卡信息，记住对应80211ad网卡的网卡接口名。例为wlp5s0

######################update###################################
#安装多网卡之后，会出现许多借口名，例如wlp5s0，wlp10s0，wlp9s0等等，这就需要我们分辨出那个才是我们想要配置的接口（iwconfig做不到）。方法如下：
dmesg
#查看log信息，得到在加载了wil6210的接口名，即为802.11ad网卡接口。

################################################################
	 Sudo apt-get install hostapd

#此时在  /etc  中生成了一个hostapd文件夹，将配置文件中的hostapd_11ad.conf放入该文件夹中。

可能会出现权限问题，此时

	 cd  /etc
	 
	 chmod –R 777 hostapd

	 gedit hostapd_11ad.conf    #更改hostapd_11ad.conf中的interface名，例为wlp5s0

	 sudo apt-get install isc-dhcp-server

#此时在  /etc  中有一个dhcp文件夹，将配置文件中的dhcp.conf放入该文件夹中，替换原来的文件。

（权限问题解决方法如上）

#将启动脚本initAP 放入  /bin  当中

	 cd  /bin

	 initAP                           #开启AP模式

######################update###################################
Q1：权限不够
A1：chmod  777 initAP

Q2：error，found in configuration gile hostapd.conf 
A2:多半是hostapd.conf 因为在下载过程中文件损坏，可以使用u盘拷贝。
###############################################################

此时开启的AP在重启之后才能重新配置。开启之后尚无关闭步骤，可重启电脑。



