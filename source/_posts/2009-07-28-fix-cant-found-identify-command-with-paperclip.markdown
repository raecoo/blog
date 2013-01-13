---
layout: post
title: 解决Paperclip找不到Identify的问题
---

使用Paperclip生成缩略图时偶尔会发生无法找到identify的错误,原来解决过一次,是因不ImageMagick版本的问题,今天又碰以了这个问题,因为测试环境装了四个不同版本的ImageMagick,搞的有点头大,都无法正常使用.后来发现一个小开关,立马解决掉了,比较爽!为什么原来我在使用这个开关没有这样的效果,有点怪异.

开关就是在environment配置文件里添加如下设置:
<pre><code>Paperclip.options[:command_path] = "/path/to/imagemagick/bin/directory"</code></pre>
这个问题貌似在Passenger下比较明显,这与Passenger加载路径的方式也有一定的关系.

<a href="http://www.icoretech.org/2008/07/12/passenger-aka-mod_rails-path-on-leopard">passenger-aka-mod_rails-path-on-leopard</a>
