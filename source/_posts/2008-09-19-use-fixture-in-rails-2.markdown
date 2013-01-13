---
layout: post
title: use fixture in rails 2
---

以往在使用Fixture时都是用部分数据填充来模拟达到真实效果,但Model之间的关系使的维护与书写Fixture成为一件比较复杂的事情,稍有不慎,Fixture也会使测试代码变的十分脆弱,今天看到一个不错的方式,基本上可以解决这个问题.方法如下:
<pre><code>
# products.yml
couch:
  name: Couch
  price: 399.99
  manufacturer: lazyboy
  categories: furniture
tv_stand:
  name: TV Stand
  price: 149.95
  manufacturer: highdeph
  categories: furniture, electronics
# manufacturers.yml
lazyboy:
  name: LazyBoy
highdeph:
  name: HighDeph
# categories.yml
furniture:
  name: Furniture
electronics:
  name: Electronics
</code></pre>
感兴趣的朋友还可以看视频教程,相信会有所收获
<a href="http://railscasts.com/episodes/81" target='_blank'>video tutorial</a>
