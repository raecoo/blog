---
layout: post
title: Operation MySql in Ruby Script
---

通过Ruby脚本直接操作数据库，代码简洁，速度快，感觉一个字：爽~ 不过要注意一下编码问题，啥时候所有环境下都默认是UTF-8的多好，贴点代码示例：
<pre><code>require 'mysql'
conn = Mysql.new("192.168.1.5", "user_name", "pasword", "database_name")
conn.query("SET NAMES UTF8")
conn.query("SET Character set utf8")
conn.query("SQL STATEMENT AT HERE")</code></pre>
