---
layout: post
title: process base64 encode in ruby
---

在Ruby世界中,语言本身就支持标准的Base64编码实现,而且还有不止一种实现,一个是类库base64中提供的实现(使用时需要require),一个是Ruby基础数据类型Array提供的,可直接使用.具体使用方法如下:

使用Array的实现
<pre><code>str = "imabase64encode"
base64_str = [str].pack("m")
original = base64_str.unpack("m") </code></pre>

使用Base64的实现
<pre><code>require "base64"
enc   = Base64.encode64('Send reinforcements')
plain = Base64.decode64(enc)</code></pre>
请注意方法pack('m')、unpack('m')以及encode64和decode64的用法

建议使用Array方式的实现,在Ruby1.9中将会去除Base64这个类库 :)
