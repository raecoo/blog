---
layout: post
title: rails store format in memcache
---

在Rails开发过程中，经常需要查看Memcache的存储内容，原来一直通过console方式，但速度太慢，效果不好，今天试图用Telnet去查看。说干就干
<pre><code>telnet 127.0.0.1 11211
get 'user_login'
ERROR</code></pre>
奇怪，不应该呀，这个Key明显是存到Cache里了，重新打开console模式测试，可以正常取出。这里有点怀疑Rails写入Memcache的机制，是不是加了类似保存Session时的前缀啊。
怎么直接查看Memcache已保存的所有Key,Google之发现使用 <strong>stats cachedump slab_id limit_num</strong>可以直接查看Memcache某个slab中的前limit_num个key列表，显示格式如下
<pre><code>ITEM key_name [ value_length b; expire_time|access_time s]</code></pre>
嗯，很爽，果不出所料，Rails确实在存入Memcache前做了点手脚，加了一个前缀。现在将前缀加上再取，成功！
<pre><code>stats cachedump 1 10
ITEM active_record:friends:86799 [1 b; 1224840079 s]
ITEM p1_cn-production:ticker_key [4 b; 1224839825 s]
ITEM p1_cn-production:timer_key [4 b; 1224839825 s]
get p1_cn-production:active_record:friends:86799
VALUE p1_cn-production:active_record:friends:86799 0 75
[iP?i恑a?i}?i劽i惷i旅i?i竺i0?iK?i     i~igit?i睹</code></pre>
可以看出前缀是根据Rails项目名称和运行模式生成的，还挺聪明
