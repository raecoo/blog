---
layout: post
title: Rails开发的20个"No"
---

<a href="http://www.chadfowler.com">chadfowler</a> 在Twitter中发起了一个在Rails编码中总会被认为是错误的提问,回应者不少,最终总结了以下20个不好的做法:
01 在视图中编码
02 使用Tab代替空格及格式错误的缩进
03 无效或遗漏的测试
04 错误的使用多态关联与单表继承
05 粗暴的异常处理<!--more-->
06 意外的本地变量赋值
07 代码中产生Ruby警告信息
08 Code that uses the features of Rails
09 滥用 validates_uniqueness_of
10 在错误的地方编码
  * 避免在视图或Helper的代码中引起数据库查询
  * 不要在Model里产生HTML
  * 不算respond_to块的代码尽可能的将Action的代码压缩在5行或更少的范围
11 在配置文件中包含自定义环境
12 太多的代码
13 混乱的$LOAD_PATH
14 模糊的逻辑
15 在Migration脚本中做数据初始化
16 在GET请求中传递数据
17 不使用事务操作
  if foo.save && bar.save
18 错误的使用JavaScript
19 大而长的方法
20 多余的注释
<a href="http://www.chadfowler.com/2009/4/1/20-rails-development-no-no-s">原文地址</a>
印象最深的就是看到多态关联被应用于一个Application使用度最频繁的评论功能,导致大于5个对象的所有评论挤在一个巨大无比的表中,查询的速度自然也就可想而知了...
关于多态关联保存数据我一直认为仅在处理应用原型阶段时可以当作玩具使用,用在真正的应用中那就是自宫的表现.
