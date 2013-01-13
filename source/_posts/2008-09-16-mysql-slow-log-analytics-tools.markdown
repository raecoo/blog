---
layout: post
title: MySql Slow Log Analytics tools
---

mysql slow log 是用来记录执行时间较长(超过long_query_time秒)的sql的一种日志工具.
启用 slow log
有两种启用方式:
1, 在my.cnf 里 通过 log-slow-queries[=file_name]
2, 在mysqld进程启动时,指定--log-slow-queries[=file_name]选项
比较的五款常用工具
mysqldumpslow, mysqlsla, myprofi, mysql-explain-slow-log, mysqllogfilter
<!--more-->
mysqldumpslow, mysql官方提供的慢查询日志分析工具.
主要功能是, 统计不同慢sql的
出现次数(Count),
执行最长时间(Time),
累计总耗费时间(Time),
等待锁的时间(Lock),
发送给客户端的行总数(Rows),
扫描的行总数(Rows),
用户以及sql语句本身(抽象了一下格式, 比如 limit 1, 20 用 limit N,N 表示).

mysqlsla, hackmysql.com推出的一款日志分析工具(该网站还维护了 mysqlreport, mysqlidxchk 等比较实用的mysql工具)
整体来说, 功能非常强大. 数据报表,非常有利于分析慢查询的原因, 包括执行频率, 数据量, 查询消耗等.

格式说明如下:
总查询次数 (queries total), 去重后的sql数量 (unique)
输出报表的内容排序(sorted by)
最重大的慢sql统计信息, 包括 平均执行时间, 等待锁时间, 结果行的总数, 扫描的行总数.

Count, sql的执行次数及占总的slow log数量的百分比.
Time, 执行时间, 包括总时间, 平均时间, 最小, 最大时间, 时间占到总慢sql时间的百分比.
95% of Time, 去除最快和最慢的sql, 覆盖率占95%的sql的执行时间.
Lock Time, 等待锁的时间.
95% of Lock , 95%的慢sql等待锁时间.
Rows sent, 结果行统计数量, 包括平均, 最小, 最大数量.
Rows examined, 扫描的行数量.
Database, 属于哪个数据库
Users, 哪个用户,IP, 占到所有用户执行的sql百分比

Query abstract, 抽象后的sql语句
Query sample, sql语句

除了以上的输出, 官方还提供了很多定制化参数, 是一款不可多得的好工具.

mysql-explain-slow-log, 德国人写的一个perl脚本.
http://www.willamowius.de/mysql-tools.html

功能上有点瑕疵, 不仅把所有的 slow log 打印到屏幕上, 而且统计也只有数量而已. 不推荐使用.
mysql-log-filter, google code上找到的一个分析工具.提供了 python 和 php 两种可执行的脚本.
http://code.google.com/p/mysql-log-filter/
功能上比官方的mysqldumpslow, 多了查询时间的统计信息(平均,最大, 累计), 其他功能都与 mysqldumpslow类似.
特色功能除了统计信息外, 还针对输出内容做了排版和格式化, 保证整体输出的简洁. 喜欢简洁报表的朋友, 推荐使用一下.
myprofi, 纯php写的一个开源分析工具.项目在 sourceforge 上.
http://myprofi.sourceforge.net/

功能上, 列出了总的慢查询次数和类型, 去重后的sql语句, 执行次数及其占总的slow log数量的百分比.
从整体输出样式来看, 比mysql-log-filter还要简洁. 省去了很多不必要的内容. 对于只想看sql语句及执行次数的用户来说, 比较推荐.
总结
