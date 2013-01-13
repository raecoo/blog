---
layout: post
title: Ruby中require,load,include以及extend的用途及区别
---

Ruby 中 “require”, “load” 和 “include” 有什么不同呢?

“require” 和 “load” 用途是一致的, 用来加载指定类库, “include” 是用来 mix-in 模組.
* “require” 可载入某个 a.rb 檔案, 且可以省略 ”.rb”. 而且它只会在第一次的時候加载, 若再次 “require” 时就会忽略
<pre><code> require 'a'
a = A.new</code></pre>
* “load” 和 “require” 一样但要用 a.rb 全名, 且每次一定都会重新加载
<pre><code> load 'a.rb'
a = A.new</code></pre>
* 加载程序库的順序呢(类型 java class path)? Ruby 把這個路径存在 ”$:” 系統全局变量当中, 你可以借助RUBYLIB 或 ruby -I 来添加新的加载路径.
<pre><code> puts $:</code></pre>
* “include” 用来 mix-in 某个模組, 可以减少代码量,更主要的是提高代码的复用
<pre><code> require 'webrick'
include WEBrick
//可以不用 server = WEBrick::HTTPServer.new(...)
server = HTTPServer.new(...)</code></pre>
<!--more-->
Ruby中的extend又是怎么回事呢?
在我看来extend可以认为是Ruby中实现多重继承的一种方式.
* extend Mix-in指定Module的方法是在类级别的,就是说这些方法用于类方法或静态方法的作用域中
* include Mix-in指定Module的方法是在对象级别的,就是说这些方法用于对象实例方法的作用域中

<a target='_blank' href="http://www.javaeye.com/topic/117925">查看代码示例</a>
