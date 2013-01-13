---
layout: post
title: 为所有HTML标签添加Hover效果
---

在制作网页时经常会用到onmouseover和onmouseout效果来改善用户体验，最常见的就是在指定Element中添加如下的代码来实现背景色的切换。
<pre><code>onmouseover='this.style.background=#666;' onmouseout="this.style.background=#fff;"</code></pre>
其实到达这个效果有两种方式：Javascript和CSS，上面提到是用JS来完成的，我个人更喜欢用CSS来解决类似问题。
用CSS的hover来解决这个问题，不仅简单高效，关键是低侵入性，页面上不会写太多东西。例如在li上添加这个效果：
<pre><code>li {background:#fff;}
li:hover {background:#666;}</code></pre>
这样的代码看起来简洁且方便日后维护，但也有一个问题就是在IE6下并不是所有HTML标签都支持hover这个属性，还好已经有人为IE做了这个Pacth，只需要添加一下就好了。
Reference: <a href="http://www.xs4all.nl/~peterned/csshover.html">http://www.xs4all.nl/~peterned/csshover.html</a>
