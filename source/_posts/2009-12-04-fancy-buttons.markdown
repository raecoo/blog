---
layout: post
title: 使用Fancy-Buttons制作漂亮的按钮
---

<a href="http://github.com/imathis/fancy-buttons"><img src="http://s3.imathis.com/dev/compass/fancy-buttons/demo.png" alt="Fancy Buttons" /></a>

Fancy Buttons是一个优雅的按钮样式生成器, 正如上图所示, 用它可以制作出多种漂亮的按钮.

安装
<pre><code>$sudo gem install fancy-buttons compass-colors</code></pre>

独立使用
<pre><code>$compass -r compass-colors -r fancy-buttons -f fancy-buttons your_project_name</code></pre>

与Rails集成
<pre><code>$compass --rails -r compass-colors -r fancy-buttons -f fancy-buttons --css-dir=public/stylesheets --sass-dir=app/sass . </code></pre>
