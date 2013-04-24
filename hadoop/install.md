---
layout: page
category: hadoop
name: install
title: 安装
---

#### 下载
[Apache Hadoop](http://hadoop.apache.org/releases.html#Download)

#### 安装SSH：Hadoop通过SSH进行通信
{% highlight bash %}
$ sudo apt-get install openssh-server
$ sudo /etc/init.d/ssh start
$ ps -e | grep ssh
{% endhighlight %}

#### 生成私钥和公钥
{% highlight bash %}
$ ssh-keygen -t rsa -P ""
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ ssh localhost
{% endhighlight %}

#### 添加hadoop用户
{% highlight bash %}
$ sudo addgroup hadoop  
$ sudo adduser --ingroup hadoop hadoop
$ sudo usermod -aG admin hadoop
{% endhighlight %}

#### 解压
{% highlight bash %}
$ sudo tar zxvf hadoop-1.1.2.tar.gz -C /opt
$ sudo chown -R hadoop:hadoop /opt/hadoop-1.1.2
$ sudo ln -sf /opt/hadoop-1.1.2 /opt/hadoop
{% endhighlight %}

#### 配置

* 配置conf/core-site.xml：指定NameNode的主机名与端口

{% highlight xml %}
<configuration>
	<property>
		<name>fs.default.name</name>
		<value>hdfs://localhost:9000</value>
	</property>
	<property>
		<name>hadoop.tmp.dir</name>
		<value>/tmp/hadoop/hadoop-${user.name}</value>
	</property>
</configuration>
{% endhighlight %}

* 配置conf/hdfs-site.xml：指定HDFS的默认副本数

{% highlight xml %}
<configuration>
	<property>
		<name>dfs.replication</name>
		<value>3</value>
	</property>
</configuration>
{% endhighlight %}

* 配置conf/mapred-stie.xml：指定JobTracker的主机名与端口

{% highlight xml %}
<configuration>
	<property>
		<name>mapred.job.tracker</name>
		<value>localhost:9001</value>
	</property>
</configuration>
{% endhighlight %}

* 配置conf/hadoop-env.sh

{% highlight bash %}
export JAVA_HOME=/opt/jdk7
export HADOOP_HOME=/opt/hadoop
export PATH=$PATH:/opt/hadoop/bin
{% endhighlight %}

#### 格式化namenode：首次运行才需要执行
{% highlight bash %}
$ cd /opt/hadoop/bin
$ hadoop namenode -format
{% endhighlight %}

#### 启动停止服务
{% highlight bash %}
$ cd /opt/hadoop/bin

$ start-dfs.sh     # 启动HDFS
$ start-mapred.sh  # 启动MapReduce
$ start-all.sh     # 启动全部

$ stop-dfs.sh      # 停止HDFS
$ stop-mapred.sh   # 停止MapReduce
$ stop-all.sh      # 停止全部

$ jpa              # 查看服务进程
{% endhighlight %}
