---
layout: post
title: Deploy Merb/Rails applicaitons with Nginx and FastCGI
---

自从用Rails做开发以来,对应用程序的部署方式也比以前有了进一步的了解,也不乏用过其中几种.我个人比较喜欢Lighttpd+FastCGI,现在公司用的是Nginx+Mongrel Cluster.

后者在公司的运用过程中也是多次在服务器负载并不大的情况下Mongrel莫名其妙假死,造成网站访问其慢无比,N多的请求都在排队,当然这里面也有一部分Mongrel本身实现机制的问题(有机会再扯一把),今天要部署一组Merb写的应用,所以基于上述的两个方式又做了一个新的调整,用Nginx+FastCGI来部署.<!--more-->

Nginx本身很好的支持了FastCGI,但多数情况下,在基于Nginx这个方案里,大家都会选择用Mongrel来支撑Merb/Rails程序,FastCGI支持PHP程序,BTW,我对Mongrel的印象特别的差,还不是一点,哈哈...我自然也就放弃了这个"杂种".
Nginx的安装就不多说的,在Debian系的发行版上一条命令搞定,<a href="http://www.raecoo.com/2009/02/08/install-fastcgi-on-ubuntu/">FastCGI的安装看这里</a>.

在这里重点介绍一下虚拟机的配置,上文件先:
<pre><code>server {
    listen       80;
    server_name platform.cyana.local;
    root /home/raecoo/works/cyana/platform/public;
    index  index.html;
    access_log  /home/raecoo/works/cyana/platform/log/access.log;
    error_log   /home/raecoo/works/cyana/platform/log/error.log notice;
    location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|html)$ {
        access_log        off;
        expires           30d;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
    # filter statics files
    location ^~/(images|javascripts|stylesheets)$ {
        root /home/raecoo/works/cyana/platform/public;
    }
   # 重点在这部分
    location / {
        include /etc/nginx/fastcgi_params;
        fastcgi_pass   platform.cyana.local:5003;
        fastcgi_index  index.html;
        fastcgi_param  SCRIPT_FILENAME /home/raecoo/works/cyana/platform/public/$fastcgi_script_name;
    }
}</code></pre>

现在重启Nginx上述的配置就加载并应用了,但现在访问会报错,原因是相应的FastCGI进程并没有启动,Nginx虽然对FastCGI支持的很好,但并不会主动控制其进程,所以我们需要一个脚本来控制这些FastCGI进程.这里我们需要用到Lighttpd源码包里提供的一个小工具Spawn-fcgi,<a href="http://www.lighttpd.net/download/lighttpd-1.4.20.tar.gz">下载Lighttpd</a>,执行
<pre><code>./configure;make;cp spawn-fcgi /usr/bin/spawn-fcgi</code></pre>生成这个脚本程序,并将其复制到用户路径下.以后就用这个家伙控制FastCGI进程了,接下来,我们再自己写一个针对应用的脚本.
<pre><code>#!/bin/sh
DISPATCH_PATH=/home/raecoo/works/cyana/platform/public/merb.fcgi
SOCKET_PATH=/tmp
ENV=development
export ENV
case "$1" in
	start)
	for num in 0 # 这里可以有多个
	do
		spawn-fcgi -a 127.0.0.1 -F 1 -p 5000 -f $DISPATCH_PATH
	done
	;;
	stop)
	#killall -9 merb.fcgi
	kill -9 $(ps -ef |grep "cyana-platform" | awk '{print $2}')
	;;
	restart)
	$0 stop
	$0 start
	;;
	*)
	echo "Usage: service.sh {start|stop|restart}"
	;;
esac
exit 0</code></pre>
把这个脚本放到应用的根目录里,以后启动和停止服务就靠它了,而且不需要重新启动Nginx.
