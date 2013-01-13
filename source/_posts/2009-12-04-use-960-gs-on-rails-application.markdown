---
layout: post
title: 在Rails应用中使用960.gs CSS框架
---

本文介绍通过 <strong><a href="http://compass-style.org/">Compass</a></strong> 以 <strong><a href="http://sass-lang.com/">Sass</a></strong> 方式集成960.gs与Rails应用程序.

1. 安装相关gem
<pre><code>$sudo gem install compass compass-960-plugin</code></pre>

2. 生成Rails应用程序, 并绑定960.gs
<pre><code>$rails 960-demo
$cd 960-demo
$compass --rails -f 960 . --css-dir=public/stylesheets --sass-dir=app/sass -r ninesixty</code></pre>

OK, 集成结束. 
