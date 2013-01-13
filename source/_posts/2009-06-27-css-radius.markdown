---
layout: post
title: CSS圆角效果
---

一直以来做圆角效果都是通过图片“加工”出来了，很是不方便，网上也有不少CSS的例子，左一个span，右一个span的，套的人头都晕了，现在用CSS3的属性就可以直接做出圆角，而且很漂亮，不过IE对CSS3并不支持，所以还需要一个Hack，好在已经在外国朋友做了这样的事，写了一个名叫<a href="http://www.dillerdesign.com/experiment/DD_roundies/">DD_roundies</a>的JS脚本，测试了一下，效果还不错。
以下代码兼容Firefox,Chrome,Safari
<pre><code>-moz-border-radius: 5px;
-webkit-border-radius:  5px;
-khtml-border-radius: 10px;
border-radius:  5px;</code></pre>
加上前面提到的JS脚本在IE下也可以做到如上的圆角效果
<pre><code>/* IE only */
  DD_roundies.addRule('.class_name_at_here', '10px');
  /* varying radii, IE only */
  DD_roundies.addRule('.class_name_at_here', '10px 4px');
  /* varying radii, "all" browsers */
  DD_roundies.addRule('.class_name_at_here', '5px', true);
</code></pre>

<pre><code>  -moz-border-radius-topright: 3px;
  -webkit-border-top-right-radius:3px;
 -khtml-border-radius-topleft: 10px;</code></pre>
