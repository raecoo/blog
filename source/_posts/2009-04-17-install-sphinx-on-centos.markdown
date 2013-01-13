---
layout: post
title: install Sphinx on CentOS
---

在开发Rails程序时做全文检索自然也就少不了<a href="http://www.sphinxsearch.com">Sphinx</a>了,如下记录了在一下裸CentOS下安装支持中文的Sphinx过程.
1.安装编译环境及相关依赖包
<pre><code>yum install gcc gcc-c++
yum install mysql mysql-devel mysql-server python-devel</code></pre>
没有试过不安装mysql mysql-server是否可行,mysql-devel是需要的

2.下载相关源码包
<a href="http://www.coreseek.com">Cooreseek</a> 基于Sphinx并添加了对中文的支持(国人出品,赞一个先)
http://www.coreseek.com/
主要下载两个源码包MMseg(中文分词库)和Coreseek(打了中文支持补丁的Sphinx),要注意版本的匹配,否则可能会出现无法编译的情况.这里我们采用了 mmseg3_0b3.tar.gz 和 csft3.1b3.tar.gz

3.编译安装
<pre><code> tar -zxvf mmseg3_0b3.tar.gz
cd mmseg3_0b3.tar.gz
./configure &amp;&amp; make &amp;&amp; make install
#安装mmseg的Ruby扩展
cd ruby
cp /usr/local/include/mmseg/*.h .
cp ../src/*.h .
cp ../src/css/*.h .
ruby extconf.lin.rb
make && make install
--------
tar -zxvf csft3.1b3.tar.gz
cd csft3.1b3.tar.gz
CPPFLAGS=-I/usr/include/python2.4 LDFLAGS=-lpython2.4 ./configure
make &amp;&amp; make install</code></pre>
比较爽的是这两个版本的源码包已经修复以前版本在编译时就会报错缺少类库的Bug,不用再手动修改一些源文件了.
Update:
编译MMSeg的过程中可能出现如下错误：
<pre><code> css/UnigramCorpusReader.cpp:89: error: ’strncmp’ was not declared in this scope</code></pre>
需要手动修改一下src/css目录下UnigramCorpusReader.cpp 文件，在第一行添加 #include "string.h"。
MMSeg安装完后还需要对 /usr/local/mmseg/include/mmseg/freelist.h文件进行编辑，添加 #include "string.h" 在第一行

在Ubuntu下编译csft时可以不用设置CPPFLAGS和LDFLAGS，直接./configure即可。
编译csft时可能会出现的问题：
<pre><code>sphinxutils.cpp:793: error: cannot convert ‘int*’ to ‘Py_ssize_t*’ for argument ‘2’ to ‘int PyDict_Next(PyObject*, Py_ssize_t*, PyObject**, PyObject**)’
sphinxutils.cpp:802: warning: unused variable ‘nRet’</code></pre>
同样还是手动编辑src目录下的 sphinxutils.cpp 修改第789行左右
int pos = 0; ———&gt;将此行修改为   Py_ssize_t pos = 0;
