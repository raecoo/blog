---
layout: post
title: Ubuntu下Flash中文显示为方块字
---

因为字体设置的缘故,网页中Flash的中文变成了方块字,Google后发现只要删除
<pre><code>/etc/fonts/conf.d/49-sansserif.conf</code></pre>
这个文件就OK了
