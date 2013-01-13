---
layout: post
title: JavaScript的模板新秀-Jaml
---

在WEB开发中用JS处理前端数据并套用一定格式的模板是件很平常的事情, 之前曾使用JSONT来做为模板引擎. 今天发现一个新玩意, 可以像书写HAML一样书写模板, 数据渲染也支持单记录, 数据, 并且对JS对象支持友好, 这样配合JSON使用感觉很好. 调用也只需要添加一个体积较小的JS库即可.

定义模板:
<pre><code>Jaml.register('product', function(product) {
  div({cls: 'product'},
    h1(product.title),
    p(product.description),
    img({src: product.thumbUrl}),
    a({href: product.imageUrl}, 'View larger image'),
    form(
      label({for: 'quantity'}, "Quantity"),
      input({type: 'text', name: 'quantity', id: 'quantity', value: 1}),
      input({type: 'submit', value: 'Add to Cart'})
    )
  );
});</code></pre>
<!--more-->

渲染数据:
<pre><code>//this is the product we will be rendering
var bsg = {
  title      : 'Battlestar Galactica DVDs',
  thumbUrl   : 'thumbnail.png',
  imageUrl   : 'image.png',
  description: 'Best. Show. Evar.'
};

Jaml.render('product', bsg);</code></pre>

渲染结果:

<pre><code>< div class="product">
  < h1>Battlestar Galactica DVDs</h1>
  < p>Best. Show. Evar.</p>
  < img src="thumbnail.png" />
  < a href="image.png">View larger image</a>
  < form>
    < label for="quantity">Quantity</label>
    < input type="text" name="quantity" id="quantity" value="1"></input>
    < input type="submit" value="Add to Cart"></input>
  < /form>
< /div></code></pre>




Reference: <a href="http://github.com/edspencer/jaml" target='_blank'>http://github.com/edspencer/jaml</a>

