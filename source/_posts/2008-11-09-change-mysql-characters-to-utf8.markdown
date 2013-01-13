---
layout: post
title: change mysql characters to utf8
---

<pre><code>raecoo@laptop:~$ mysql -uroot -p
mysql> show variables like 'character%';
+--------------------------+----------------------------+
| Variable_name                 | Value                      |
+--------------------------+----------------------------+
| character_set_client         | latin1                       |
| character_set_connection  | latin1                       |
| character_set_database    | latin1                       |
| character_set_filesystem   | binary                     |
| character_set_results        | latin1                       |
| character_set_server        | latin1                       |
| character_set_system       | latin1                       |
| character_sets_dir            | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+</code></pre>
mysql default characters is latin1,so we need update it to utf8 by my.cnf.
go to directory /etc/mysql/ and open the my.cnf config file,modify like this:
<pre><code>[client]
default-character-set=utf8
[mysqld]
default-character-set=utf8
init_connect='SET NAMES utf8' </code></pre>
then restart mysql server ,to see the results of the revised.
<pre><code>raecoo@laptop:~$ mysql -uroot -p
mysql> show variables like 'character%';
+--------------------------+----------------------------+
| Variable_name                 | Value                      |
+--------------------------+----------------------------+
| character_set_client         | utf8                       |
| character_set_connection  | utf8                       |
| character_set_database    | utf8                       |
| character_set_filesystem   | binary                     |
| character_set_results        | utf8                       |
| character_set_server        | utf8                       |
| character_set_system       | utf8                       |
| character_sets_dir            | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+</code></pre>
