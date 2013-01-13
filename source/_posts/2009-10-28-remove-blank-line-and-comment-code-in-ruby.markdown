---
layout: post
title: 去除Ruby代码中的空行与注释
---

正则表达式去除空行与注释代码
<pre><code># 空行
^\s*(?<=\n)
# 注释
^\s*#.*$</code></pre>
