---
layout: post
title: upgrade merb cause nothing to render
---

今天看到Merb有版本更新就顺手更新了一下,正好要写一个关于RESTFul的小脚本,随即生成一个新的App,但不知道怎么搞的不管是手工生成的Controller还是用resource生成的资源都无法正确渲染内容.

在测试过程中为Action添加了before,end过滤器,过滤器内中的日志反馈得知前置过滤器正确执行,后置过滤压根没反应,Action里的日志也一样默默无闻,郁闷,找了半天的原因,愣是没发现,后来直接上Maillist发现也有人提类似的问题.有人反馈是merb-action-args引起的问题.随即在dependencies.rb中将它注释掉,重启App发现OK了,问题确实在此.

看起来这个小玩意还不完善,我也顺手把测试环境补在了Maillist里,希望社区尽快有相关的patch出来,以下是测试环境
<pre><code>Ubuntu 8.10
ruby 1.8.7 (2008-08-11 patchlevel 72) [i486-linux]
merb (1.0.6.1)
merb-action-args(1.0.6.1)</code></pre>
