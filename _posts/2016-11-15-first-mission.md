---
layout: post
title:  "高通毫米波网卡配置"
date:   2016-11-15 00:06:05
categories: 网卡
tags: 高通 网卡 毫米波
---

* content
{:toc}

## 问题描述
新拿到了一个60GHz毫米波网卡（），老师让我配置一下。从来没接触过，有点难哎。不过整体已经配置完毕了，下面说一下我的配置过程吧。
# (一)	前言
本文将主要叙述一下网卡“QCA9008-TBD1”的配置安装过程。硬件安装详见硬件部分。在整个配置过程当中，会遇到好多好多的问题，因为ubuntu强大的安全性，会有很多权限问题出现，同时涉及到硬件部分会有很多意想不到的error。这款网卡又是较为少见的硬件，google也不是万能的，这就需要有强大的内心。本人在配置过程中一度走到死角(初期以为需要配置内核，结果一个问题套着一个问题无穷尽，最后整个电脑当掉了只好重装系统)，最后在一次次尝试当中总结出了安装的正确途径。特此记录，以遗来者。
# (二)	内核问题
我们正常安装的ubuntu内核一般很老，并且没有对特定的硬件设备进行适配，如我们所使用的QCA9008网卡，需要内核当中的特定驱动来配合固件完成对网卡的操作（待研究？）。高通在网络上有一个专门对此网卡的优化内核网址。https://git.kernel.org/pub/scm/linux/kernel/git/kvalo/ath.git/
我们可以按照一些步骤将内核替换成这个内核以完成对网卡的适配，步骤如下：
* 以下均是在ubuntu的root权限之下的终端操作
* 步骤参考网址：https://wiki.ubuntu.com/KernelTeam/GitKernelBuild
* 以下过程需要在联网情况下完成（需要耗费大量流量、时间）
	 sudo apt-get update

	 sudo apt-get install git build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache

	 cd $HOME

	 git clone git://git.kernel.org/pub/scm/linux/kernel/git/kvalo/ath.git

	 cd linux

	 git checkout COMMIT

	 cp /boot/config-`uname -r` .config

	 make oldconfig

     make clean

     make -j5 `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-custom

     cd ..

     sudo dpkg -i linux-image-2.6.24-rc5-custom_2.6.24-rc5-custom-10.00.Custom_i386.deb

     sudo dpkg -i linux-headers-2.6.24-rc5-custom_2.6.24-rc5-custom-10.00.Custom_i386.deb

     sudo reboot

经测试，内核不是问题！以上并非必要（捶桌三分钟）但依然对自定义内核的安装有指导作用。
update：（2018-04-25）最近weiteng有了一个新的网卡固件，增加了很多功能，比如RSS的精确收集（每个beacon），是需要更新新的内核的，果然以前的失误说不定是以后的财富。


# (三)	固件问题
在硬件安装之后，我们在ubuntu中能看到有两个网卡，其中80211ad网卡显示“固件缺失”此时需要我们将该网卡的固件手动放置到正确位置。

将配置文件中的wil6210.brd和wil6210.fw放到   /lib/firmware   中。（需要root权限，更改/lib 权限  chmod –R 777 /lib）.

     sudo cp –i wil6210.brd lib/firmware
     sudo cp –I wil6210.fw llib/firmware

重启，可看到“固件缺失”提示消息不见，此时固件成功。但是网卡没有可操作性。为了操作网卡发射信号，接收数据，我们需要将其中的一个网卡配置成AP模式，也就是我们常说的热点，只不过是使用60GHz。


