---
layout: post
title: 灵活使用ActiveRecord的AutosaveAssociation
---

在对表单进行验证时ActiveRecord自身提供了很棒的验证机制.本文在此主要介绍一下单一表单提交多个有关联关系的模型验证.

来一个简单的场景, 社区主题与回复是一个典型的一对多的关系,通常会将主题的标题和一些基本信息放置在topic模型中,而主题的内容与回复放置于post模型,所以看起来表结构基本如下(此处忽略一切关键字段):
<!--more-->
<pre><code>  create_table "topics", :force => true do |t|
    t.string   "title"
  end

  create_table "posts", :force => true do |t|
    t.integer  "topic_id"
    t.text     "body"
  end</code></pre>
也就是说当创建一个主题将会在topics & posts两个表中各插入一条记录, 当然回复仅涉及posts一个表.
显然在创建主题时标题与内容都不能为空,所以我们需要对这两个字段添加验证(所有涉及代码均在本文结尾显示).

提到单表单中的多个模型验证, 这里既涉及到事务,也涉及到验证信息的反馈, 具体的方法在<a href="http://www.javaeye.com/topic/238160">在rails中优雅的进行模型校验</a>一文中也有激烈的讨论.方法是多种多样的,适用的场景也各不相同,视情况而定.
我个人更倾向于autosave这种方式来处理级联模型的验证,特点当然是:简洁,易懂. 这一点可以在随后的代码中得以体现.

回到本文的场景中,当没有填写主题内容而提交表单时,验证信息会显示为 <strong>Posts body can't be blank</strong>, 这其中的Posts body并不是topic模型的属性,而是autosave将post模型的验证信息以级联对象的方式添加到了topic模型的验证返回信息中,且因为二者是一对多的关系,所以是Posts,如果是一对一则是Post. 这样验证的目的是达到了,但不好友的验证信息会使人搞不清楚到底topic还是post,所以在此需要做点文章.

此示例中我是通过rails 自带的I18n来实现上述的目的. 也就是人为的为topic添加一个名为<strong>posts_body</strong>的虚拟的属性验证信息,这样当提交表单时,相应的错误信息就显示i18n中所定义信息. 想写成什么样,随便你喽~ 不过至少不会让用户发晕~

以下是示例代码:
<script src="http://gist.github.com/184413.js"></script>
API说明请移步至: <a href="http://api.rubyonrails.org/classes/ActiveRecord/AutosaveAssociation.html">http://api.rubyonrails.org/classes/ActiveRecord/AutosaveAssociation.html</a>
