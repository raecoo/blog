---
layout: post
title: 比tail更实用的less
---

<pre><code>tail -f development.log</code></pre>
<pre><code>less +F development.log</code></pre>
简单的看这两条命令没什么区别,但实际上后者比前者还是强大不少,起码需要在log里查找内容时不再需要C+c,然后用vim干活,而只需要简单的按一下C+c进入编辑模式,接下来的操作就和vim完全一样,hjkl, / 统统可以用上,完活后Shift+f返回log的监听模式.

出处: <a href="http://blog.libinpan.com/2009/07/less-is-better-than-tail/">http://blog.libinpan.com/2009/07/less-is-better-than-tail/</a>
