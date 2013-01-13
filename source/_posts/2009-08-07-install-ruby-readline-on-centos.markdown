---
layout: post
title: install ruby readline on centos
---

first, install the readline header file
<pre><code>yum install readline-devel</code></pre>
the second, install ruby readline
<pre><code>cd /ruby/src/package/ext/readline/directory
ruby extconf.rb
make && make install</code></pre>
