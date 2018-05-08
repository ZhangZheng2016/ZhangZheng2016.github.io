---
layout: post
title:  "NAN问题"
date:   2018-01-08 19:24:37
categories: 机器学习
tags: NAN 机器学习 调参
---

* content
{:toc}



在我们一个非线性回归预测项目当中，出现了无法解决的NAN问题

我们使用的是pytorch深度学习框架，搭建的是一个无卷积层的神经网络，这个全连接网络由五层隐藏层组成，使用的训练数据保证是有效且无坏数据的（matlab环境仿真生成，可以在一定程度上保证我们数据不会产生坏数据，经过仔细查看问题发生数据位置，并不是坏数据）

这个问题出现的很奇怪，只有在部分数据上出现，虽然已经查看过并不是数据的问题。。。

而且只有在我们使用logsigmoid作为激活函数的时候出现，在使用ReLU时不会出现。logsigmoid在我们的测试集当中表现的非常好，已经接近99.99%的预测准确率了。

在网上搜索解决方案，但是均不能解决我们的问题。后来在另一名深度学习大牛的提醒下，进行了参数限制（提供一个取值区间，超出则重置这个数），虽然NAN问题不在出现，但是预测准确率也完全没有了。

这个问题现在仍然没有解决。只能使用ReLU得到不太好的准确度，然后再数据集上进行优化（增大），勉强达到要求准确度。

特此记录，期待解答。（以后项目完成，就把代码po出来，现在还不行...）