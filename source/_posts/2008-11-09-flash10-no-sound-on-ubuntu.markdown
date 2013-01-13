---
layout: post
title: Ubuntu中Flash 10无声音的解决方法
---

原本安装的是Flash9但总会频繁的把Firefox给搞崩溃，无奈升成Flash10，结果今天Flash播放器又没声音了，搜索了一下发现运行如下命令后就恢复正常了，真是不错
<pre><code>asoundconf set-pulseaudio</code></pre>
