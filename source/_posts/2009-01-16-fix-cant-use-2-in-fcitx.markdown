---
layout: post
title: 解决Fcitx输入法2键冲突
---

一直以来Fcitx是我在Linux下默认的输入法,但始终有个小问题就是2键时不时会有失效,猜想应该是和什么软件冲突,但从没找到解决方法,今天偶然看到一小方法试了一把,果然解决了,很好用,记录一下.
<pre><code>vim ~/.fcitx/config
第二三候选词选择键=SHIFT</code></pre>
找到上述配置项,将这个SHIFT删除,Ctrl+5重新加载配置文件,OK了,2键回来了
