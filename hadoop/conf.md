---
layout: page
category: hadoop
name: index
title: 配置
---

#### 获取默认配置
* [core-site.xml](http://hadoop.apache.org/docs/r1.1.2/core-default.html)
* [hdfs-site.xml](http://hadoop.apache.org/docs/r1.1.2/hdfs-default.html)
* [mapred-site.xml](http://hadoop.apache.org/docs/r1.1.2/mapred-default.html)

#### 常用的端口配置

* HDFS端口

|---------------------------+---------------------------+-----+-------------|
|参数						|描述						|默认  |配置文件		|
|---------------------------|---------------------------|-----|-------------|
|fs.default.name			|NameNode RPC交互端口			|8020 |core-site.xml|
|dfs.http.address			|NameNode web管理端口			|50070|hdfs-site.xml|
|dfs.datanode.address		|DataNode控制端口				|50010|hdfs-site.xml|
|dfs.datanode.ipc.address	|DataNode的RPC服务器地址和端口	|50020|hdfs-site.xml|
|dfs.datanode.http.address	|DataNode的HTTP服务器和端口	|50075|hdfs-site.xml|
|---------------------------+---------------------------+-----+-------------|
