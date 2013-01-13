---
layout: post
title: Install memcached on linux
---

首先下载需要用到的<a href="http://www.danga.com/memcached/">memcached</a> 和 <a href="http://www.monkey.org/~provos/libevent/">libevent</a>源码包.
分别编译安装
<pre><code>./configure &amp;&amp; make &amp;&amp; make install</code></pre>
安装后运行memcached
<pre><code>memcached -m 512 -u nobody -vv</code></pre>
可能会出现如下错误:
<pre><code>error while loading shared libraries: libevent-1.4.so.2: cannot open shared object file: No such file or directory”</code></pre>
错误的原因是未在系统中注册Libevent,解决方法如下
<pre><code>vi /etc/ld.so.conf.d/libevent-i386.conf
/usr/local/lib/</code></pre>
如果不喜欢这样,也可以自己做个软链接.
现在再启动就不会出此错误了.不过此时的memcached还不能开机启动,动手写一个启动脚本(仅在CentOS上测试).<!--more-->
<pre><code>#!/bin/sh
#
# memcached:    MemCached Daemon
#
# chkconfig:    - 90 25
# description:  MemCached Daemon
#
# Source function library.
. /etc/rc.d/init.d/functions
. /etc/sysconfig/network
start()
{
echo -n $"Starting memcached: "
daemon /usr/local/bin/memcached -u root -d -m 512 -P /tmp/memcached.pid
echo
}
stop()
{
echo -n $"Shutting down memcached: "
killproc memcached
echo
}
[ -f /usr/local/bin/memcached ] || exit 0
# See how we were called.
case "$1" in
start)
start
;;
stop)
stop
;;
restart|reload)
stop
start
;;
condrestart)
stop
start
;;
*)
echo $"Usage: $0 {start|stop|restart|reload|condrestart}"
exit 1
esac
exit 0</code></pre>
还需要做一些设置,此脚本就可以正式工作了.
<pre><code>chkconfig  --add memcached
chkconfig  --level 3  memcached  on
chkconfig  --list | grep mem
#memcached       0:off   1:off   2:off   3:on    4:off   5:off   6:off
/etc/rc.d/init.d/memcached  start/stop/restart  or service memcached start/stop/restart</code></pre>
