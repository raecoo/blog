---
layout: post
title: Apache+Passenger部署Rails
---

使用Apache + Passenger部署Rails应用程序很是简单，就以下几条命令即可完成！
<pre><code>$ sudo gem install passenger
$ passenger-install-apache2-module</code></pre>
添加如下三行配置到apache2.conf的文件尾部
<pre><code>LoadModule passenger_module /usr/lib/ruby/gems/1.8/gems/passenger-2.2.2/ext/apache2/mod_passenger.so
PassengerRoot /usr/lib/ruby/gems/1.8/gems/passenger-2.2.2
PassengerRuby /usr/bin/ruby1.8</code></pre>
生成虚拟主机配置文件，并添加如下配置内容：
<pre><code>sudo touch /etc/apache2/sites-available/domain.com
sudo vim /etc/apache2/sites-available/domain.com </code></pre>
<pre><code>&lt; VirtualHost *:80 &gt;
ServerName www.domain.com
ServerAdmin webmaster@domain.com
DocumentRoot /path/to/rails_app_name/public
RailsEnv development
RailsAllowModRewrite off
&lt; directory "/path/to/rails_app_name/public" &gt;
Order allow,deny
Allow from all
&lt; /directory &gt;
&lt; /VirtualHost &gt;</code></pre>
再做一个软链接并重启Apache
<pre><code>ln -s /etc/apache2/sites-available/domain.com /etc/apache2/sites-enabled/domain.com
sudo /etc/init.d/apache2 restart
</code></pre>
这个部署方式没什么好说的，就是简单，更多的优点请自行Google，做为开发环境的配置还是很不错滴~而且Rails应用程序本身不需要做什么配置，如若重启，只需要
<pre><code>touch tmp.restart.txt </code></pre>就搞定了.

添加基于域名的虚拟主机配置
<pre><code>NameVirtualHost *:80 #重点是这句
&lt; VirtualHost *:80 &gt;
ServerName www.domain.tld
ServerAlias domain.tld *.domain.tld
DocumentRoot /www/domain
&lt; /VirtualHost&gt;
&lt; VirtualHost *:80 &gt;
ServerName www.otherdomain.tld
DocumentRoot /www/otherdomain
&lt; /VirtualHost &gt;</code></pre>
