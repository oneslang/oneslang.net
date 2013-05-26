---
layout: page
category: linux
name: network
title: 网络配置
---


#### 常用命令

* ifconfig
$ ifconfig eth0 # 查看eth0的配置
$ ifconfig eth0 192.168.0.6 netmask 255.255.255.0 # 为网络接口设置IP
$ ifconfig eth0:0 192.168.0.7 netmask 255.255.255.0 # 为eth0配置第2个IP地址

* hostname
$ hostname server.evil.club # 把主机名修改为server.evil.club（只有root用户才有权限修改）

* ifup
$ ifup eth0 # 激活eth0网络接口

* ifdown
$ ifdown eth0 # 停止eth0网络接口

* service
$ service network restart
$ service --status-all # 显示系统中所有服务的运行状态



#### 与网络有关的配置文件

* 以下是“/etc/sysconfig/network-scripts/ifcfg-eth0”文件的内容

DEVICE=eth0
ONBOOT=yes
BOOTPROTO=none
IPADDR=192.168.1.8
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
TYPE=Ethernet
USERCTL=no
PEERDNS=no
NETWORK=192.168.1.0
BROADCAST=192.168.1.255

说明如下：

DEVICE=eth0 （设备名称）
ONBOOT=yes （计算机启动时是否激活网卡，取值为：yes/no）
BOOTPROTO=none   （获取IP的方式：取值为：static/bootp/dhcp）
IPADDR=192.168.1.8 （该网络接口的IP地址）
NETMASK=255.255.255.0 （子网掩码）
GATEWAY=192.168.1.1      （网关地址）
TYPE=Ethernet 
USERCTL=no
PEERDNS=no
NETWORK=192.168.1.0
BROADCAST=192.168.1.255 （广播地址）

* 以下是“etc/sysconfig/network”文件的部分内容

NETWORKING=yes
HOSTNAME=localhost.localdomain

说明如下：
NETWORKING：设置Linux是否运行网络，取值为：yes/no
HOSTNAME：设置计算机的主机名
GATEWAY：设置网关的IP地址
GATEWAYDEV：连接网关的网络设备
NISDOMAIN：NIS域名（使用NIS系统）


* 以下是“etc/resolv.conf”文件的部分内容

search localdoma
domain localdoma
nameserver 202.96.128.166
nameserver 192.168.1.1

说明如下：
search：DNS搜索路径，当解析不完整名称时默认的附加域名后缀。
domain：设置计算机的本地域名。
nameserver：设置DNS地址，客户机解析名称时会按顺序分别使用。


