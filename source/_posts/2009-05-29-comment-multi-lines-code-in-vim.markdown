---
layout: post
title: 在VIM中注释多行代码
---

用VIM也有段时间,但一直没有找到列编辑的方法,很是不爽,今天要注释一段代码,要是一行一行加,非要死人不可,查了下帮助,找到如下方法,蛮实用的.

假如要在10,20行间在第1列插入或删除一个#字符
<pre><code>:10,20s/^\(.\{0\}\)/\#/g
:10,20s/^\(.\{1\}\)//g
</code></pre>
