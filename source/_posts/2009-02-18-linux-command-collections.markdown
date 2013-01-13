---
layout: post
title: 常用Linux配置及命令
---

持续更新
---------------------------
编辑~/.bashrc,添加如下语句,即可拥有ll指令
<pre><code>alias ll='ls -l --color=auto'
source ~/.bashrc
</code></pre>

杀死指定端口进程
<pre><code>kill -9 $(netstat -tlnp|grep 1099|awk  '{print $7}'|awk -F '/' '{print $1}')</code></pre>
修改Terminal窗口大小与位置
<pre><code>gnome-terminal --geometry=110x20+50+200</code></pre>
Note: --geometry=width*height+x position+y position

<!--more-->关闭PC Speaker
<pre><code>sudo modprobe -r pcspkr
or
sudo vim /etc/modprobe.d/blacklist
# add this line
blacklist pcspkr</code></pre>
