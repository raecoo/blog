---
layout: post
title: ruby email validation regex expression
---

this Regex Expression can handle '-' character in Ruby email validation
<pre><code>^\w+((-\w+)|(\-)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$</code></pre>

Ruby Regex Expression test tool : <a href="http://www.rubular.com/" target="_blank">http://www.rubular.com/</a>

BTW：only test in ruby.

感谢<a href="http://blog.ashchan.com" target='_blank'>ashchan</a> 提供了可以支持Gmail 标签的正则表达式，经测试效果也不错，如下：
<pre><code>/^([^@\s!#\$%\^&amp;\(\)]+)@((?:[-a-z0-9A-Z]+\.)+[a-zA-Z]{2,})$/</code></pre>
