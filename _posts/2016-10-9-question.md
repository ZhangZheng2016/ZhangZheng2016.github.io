---
layout: post
title:  "ZZ-实验-未解之谜"
date:   2016-10-9 23:10:50
categories: 未解之谜
tags: 软件无线电 网卡 尚无答案
---

* content
{:toc}



1.	为什么QCA9008网卡能在我的windows下使用，而不能在XPZ和团团的电脑windows上用呢？（团团电脑和我的电脑配置完全相同）

2.	QCA9008网卡明明在dmesg log中还有好多的disconnect error存在，怎么就能连接而且还能正常传数据呢？

3.	QCA9008网卡和pem009的信号能不能互通呢?

	据周老师：pem009能检测到有60GHz的信号存在，但也仅仅是能得到一个信号强度而已，不能解析出来信号的内容（高通无线网卡信号层层包裹）。QCA网卡认证一个信号为60GHz AP 需要认证很多东西，而PEM发出来的显然是没有这些的。

4.	在维基百科中，QCA9008天线接口为MHF4，通过网络查询得到，MHF4与murata的HSC兼容，那为什么最后成功应用的反而是JSC系列呢？ 
 
	[wiki](https://wikidevi.com/wiki/Qualcomm_Atheros_QCA9008-TBD1)
	https://www.gradconn.com/Products/CoaxialCableAssembly
	可能是这个MHF4指的是普通wifi接口线型号？但是在PCIe转接器网站上面又说是MHF5接口的wigig接口。很费解。
	http://www.hwtools.net/Adapter/MP8605A-tw.html#Package_Content
	猜测答案：QCA9008两个普通wifi接口为MHF4（HSC）接口，wigig接口为JSC接口，intel的网卡与高通的网卡wigig接口不同，intel的是MHF5.

5.	PEM009-kit连接的是IQ，但是还需要在GUI中配置为FM&AM连接才有信号？？？

	猜测答案：在阅读pem001-mim之后我发现了一个需要注意的地方：There are optional FSK/MSK baseband data inputs for non-coherent modulation applications。这个non-coherent modulation非相干解调是指不需要提取载波信息的一种解调方法。通常来说，非相干解调方法，电路简单，实现容易，但是相较相干解调方法，其性能略有损失。相干解调需要接收机和载波同步；而非相干解调不使用乘法器，不需要接收机和载波同步。结合之前与北大博士的话来看由于两个前端的时钟不同步（？前端时钟跟载波有关系？），以至于在测试当中选择I 、Q channel反而检测不到信号的存在，现在之所以检测到了信号完全是因为非相干解调方式不需要使用同步的载波。所以为了更好的性能（信号质量）需要我们做到同步！（？？？）
	解决方法：1、接一个外部时钟，同步一下看看；2、


6.	为什么跑起来毫米波测试程序（waveoriginal.m），遮挡产生的信号质量、强度变化会有延时，并且随着跑程序时间的增长，这个延时会越来越长（刚开始几乎为零，一分钟后，延时变成5s左右）。
	猜测答案：USRP的buffer太小，信号数据来不及传输，而且会越积越多。



7.	ubuntu明明设置好了root密码，进入权限的时候就是认证失败。使用sudo passwd root 更换密码之后还是不行。
还不知道怎么解决嘞。


8.	在配置2.4GHz+60GHz双AP时，同时使用hostapd方法配置，可以得到两个AP网络，但是在连接之后，2.4Gwifi不能ping通网关主机。


9.	To be continue...
