---
layout: post
title:  "硬件连接-高通毫米波网卡"
date:   2016-12-15 19:52:25
categories: 网卡
tags: 高通 网卡 硬件
---

* content
{:toc}




下图为我们所使用的高通无线网卡，各接口说明如图所示：
 
![hw1](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/hw1.png)

需要将无线网卡插在电脑的PCIe接口上，需要如下转接卡：


![hw2](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/hw2.png)


 


天线阵列如下：
![hw3](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/hw3.png)

天线阵列与无线网卡连接方式如下，

![hw4](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/hw4.png)

所需连接线为ＭＨＦ５　ｔｏ　ＭＨＦ５线：
 
将上述的连接线分别连接在网卡wigig口和天线连接口之后，放在转接卡的插槽里，插在电脑的PCI-e *1接口上。重启电脑，即可在电脑配置中发现网卡。在win10中显示如下：
![hw5](https://raw.githubusercontent.com/ZhangZheng2016/ZhangZheng2016.github.io/master/_posts/picture/hw5.png)
上图中，标号为1的即时我们想要的wigig网卡，标号为2的是此网卡上集成的8011ac网卡。
在ubuntu中直接在设置》网络即可看到加载出的网卡。
