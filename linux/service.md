---
layout: page
category: linux
name: service
title: 服务管理
---

#### 方式一： 
查看服务列表代码
{% highlight bash %}
service --status-all
{% endhighlight %}


启动开机时的服务代码
{% highlight bash %}
sudo update-rc.d -f myservice default
{% endhighlight %}


停止开机时的服务代码
{% highlight bash %}
sudo update-rc.d -f myservice remove
{% endhighlight %}



#### 方式二： 
安装代码
{% highlight bash %}
sudo install sysv-rc-conf
{% endhighlight %}


执行代码
{% highlight bash %}
sudo sysv-rc-conf
{% endhighlight %}

