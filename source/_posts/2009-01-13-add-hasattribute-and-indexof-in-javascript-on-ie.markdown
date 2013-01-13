---
layout: post
title: 在Javascript中为IE添加hasAttribute,indexOf方法
---

IE没有hasAttribute这个方法,但提供了getAttribute,这就需要自己搞一把,这样hasAttribute在FF/IE下就通吃了
<pre><code>function hasAttribute(elm,attribute){
  return elm.getAttribute(attribute) != null;
}</code></pre>
Javascript中Array的默认方法里没有提供indexOf方法,那也自己动手加一个进去 :)
BTW: 以prototype方式来Hack Javascript 真的很爽
<pre><code>if (!Array.prototype.indexOf) Array.prototype.indexOf = function(item, i) {
  i || (i = 0);
  var length = this.length;
  if (i < 0) i = length + i;
  for (; i < length; i++)
    if (this[i] === item) return i;
  return -1;
};</code></pre>
