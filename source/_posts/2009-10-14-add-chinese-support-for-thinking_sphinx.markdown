---
layout: post
title: Thinking-sphinx 的中文支持
---

一直以来项目中使用的都是ultrasphinx插件做为Sphinx的接口,效果也还不错,不过一直不太喜欢ultrasphinx索引的定义方式,怎么看怎么别扭(个人习惯), 相比之下还是看thinking-sphinx顺眼些.

thinking-sphinx自身是支持utf8, 不过打了中文补丁的Sphinx编码需要设置为zh_cn.utf8,但thinking-sphinx目前并没有自定义的扩展,所以就需要hack一下, 主要为中文检查添加了两个option:
<!--more-->
<pre><code>charset_type: zh_cn.utf-8
charset_dictpath: dict/path</code></pre>
使用时只需要在sphinx.yml里做相应设置即可.

hack后的插件地址为: http://github.com/raecoo/thinking-sphinx-chinese

为了支持中文对以下三个文件进行了hack,目前看起来即使升级新版本也应该不会有什么影响.
<pre><code>lib/thinking_sphinx/configuration.rb
vendor/riddle/lib/riddle/configuration/index.rb</code></pre>
对以上两文件的修改主要是为了添加charset_dictpath这个自定义的变量,方便生成配置文件时使用
<pre><code>lib/thinking_sphinx/source.rb</code></pre>
source.rb的utf8?方法是修改的重点,此方法仅对utf-8编码进行判断. 此方法的作用是为生成的sphinx配置文件中SQL语句部分关于编码设置的一条语句. 特别是针对中文此语句也是最为重要的一句,相信遇到过编码问题的人一看就明白
<pre><code>sql_query_pre = SET NAMES utf8</code></pre>

共修改了三个文件, 添加的字符数也不到50个即可解决TS的中文检索.
