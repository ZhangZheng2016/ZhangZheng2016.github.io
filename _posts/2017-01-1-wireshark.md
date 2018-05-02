---
layout: post
title:  "网卡抓包（wireshark）"
date:   2017-01-01 18:12:15
categories: 网卡
tags: 网卡 抓包 wireshark
---

* content
{:toc}


wireshark是一个网络封包分析软件。网络封包分析软件的功能是撷取网络封包，并尽可能显示出最为详细的网络封包资料。Wireshark使用WinPCAP作为接口，直接与网卡进行数据报文交换。

	 sudo apt-add-repository ppa:wireshark-dev/stable
	 
#如果源不对的话可启用上命令。

	 sudo apt-get update

	 sudo apt-get install wireshark


#出现确认框，选择YES。

	 sudo gedit /etc/group

#在组策略中会出现wireshark组，默认没有任何用户属于这个组，只需把特定的用户加入组中就可以以该用户来运行wireshark实时抓网络数据包。



进入wireshark界面。可能会显示一个error，ignore就好了。

然后我们就能在界面上看到许多接口了，选择monitor模式（monitor模式切换，点击：[set_monitor](https://zhangzheng2016.github.io/2017/01/01/monitor/)）的那个接口名，进行抓包。


