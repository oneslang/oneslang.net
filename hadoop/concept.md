---
layout: page
category: hadoop
name: concept
title: 简介
---

### Hadoop的运行模式

* 单机模式（standalone）

	单机模式是Hadoop的默认模式。当首次解压Hadoop的源码包时，Hadoop无法了解硬件安装环境，便保守地选择了最小配置。在这种默认模式下所有3个XML文件均为空。当配置文件为空时，Hadoop会完全运行在本地。因为不需要与其他节点交互，单机模式就不使用HDFS，也不加载任何Hadoop的守护进程。该模式主要用于开发调试MapReduce程序的应用逻辑。

* 伪分布模式（Pseudo-Distributed Mode）

	伪分布模式在“单节点集群”上运行Hadoop，其中所有的守护进程都运行在同一台机器上。该模式在单机模式之上增加了代码调试功能，允许你检查内存使用情况，HDFS输入输出，以及其他的守护进程交互。

* 全分布模式（Fully Distributed Mode）

	Hadoop守护进程运行在一个集群上。
