---
layout: post
title: install the MySQL/Ruby adapter on Leopard
---

http://tmtm.org/downloads/mysql/ruby/mysql-ruby-2.8.tar.gz
<pre><code>tar -zxvf mysql-ruby-2.8.tar.gz
cd mysql-ruby-2.8
sudo env ARCHFLAGS="-arch i386" ruby extconf.rb -- \
  --with-mysql-dir=/usr/local/mysql --with-mysql-lib=/usr/local/mysql/lib \
  --with-mysql-include=/usr/local/mysql/include
make
sudo make install</code></pre>
注意:安装过程中出现无法找到lmysqlclient的提示,所以在生成编译文件时需要加一些参数
UPDATE:
sudo ruby extconf.rb -- --with-mysql_config
