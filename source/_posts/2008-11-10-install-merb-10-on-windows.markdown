---
layout: post
title: install Merb 1.0 on Windows
---

早期的Merb在Windows上安装是件很恶心的事，缺这少那的，很是不爽，Merb 1.0也正式发布了，今天正好系统重做了一下，在干净的环境下试了一把，Merb 1.0可以正常安全与运行，相比之前版本的安装好些了，但也不省事，必要安装的Gem包还是一大堆，啥时候能和Rails一样安装Rails会自动把相关包一并安装啊，或许这就是Merb可定制化这样的特点对于我这个懒人的不适应吧！ :)

<strong>安装必要的Gem</strong>
<pre><code>extlib
erubis
json_pure
rspec
rack
mime-types
thor
ruby2ruby(ZenTest RubyInline sexp_processor ParseTree)
templater(diff-lcs)
haml
mailfactory
dm-core(addressable data_objects)
dm-migrations
dm-timestamps
dm-aggregates
dm-validations
dm-sweatshop
dm-types
do_sqlite3</code></pre>
注意：括号里的gem是被附加安装的，可以不用手动安装
<!--more-->
<strong>安装Merb</strong>
<pre><code>gem install merb -s http://edge.merbivore.com</code></pre>
<strong>生成Merb应用</strong>
<pre><code>merb-gen app merbtest</code></pre>
<strong>启动应用</strong>
<pre><code>cd merbtest_directory
merb
http://localhost:4000/</code></pre>
oh~yea!  可以看到绿色的Logo了
