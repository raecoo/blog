---
layout: post
title: 安装libmemcached及memcached
---

昨天想要给Merb写的一个应用加上缓存功能,自然首选就是Memcached了,不过在配置过程中发现了一和Rails不一样的地方,记录一下!

在Rails里通常会用到memcached-client作为与Memcached通信的类库.它是一个纯Ruby的实现,用起来效果也不错,但在Merb里就不推荐使用这个东西了,而是改用<a href="http://github.com/fauna/memcached/tree/master">memcached</a>这个gem,起初犯了个错误,没仔细看文档,还以为memcached和memcached-client是一个东西,也就是因为这个疏忽导致浪费了很多时间,下次还是先看文档再动手的好.

这里会涉及到libmemcached,memcached.gem
memcached 这个gem是<a href="http://tangent.org/552/libmemcached.html">libmemcached</a>这个C实现的Memcached 客户端工具的Ruby接口.
<!--more-->
下面就是安装过程:

1. download libmemcached (http://tangent.org/552/libmemcached.html)
<pre><code>wget http://download.tangent.org/libmemcached-0.25.tar.gz
tar zxvf libmemcached-0.25.tar.gz</code></pre>
./configure ; make ; sudo make install
2. download memcached gem (http://github.com/fauna/memcached/tree/master)
<pre><code>git clone git://github.com/fauna/memcached.git
cd memcached ; sudo gem install memcached</code></pre>
3. create a symlink
<pre><code>sudo ln -s /usr/local/lib/libmemcached.so.2 /usr/lib/</code></pre>

Congratulations, install successful ~ :)

测试一下是不是安装成功 : irb -rubygems, require 'memcached'

UPDATE:
Mac下使用port安装memcached后需要手动添加一下daemon进程,方法如下:
<pre><code>sudo launchctl load -w /Library/LaunchDaemons/org.macports.memcached.plist</code></pre>
