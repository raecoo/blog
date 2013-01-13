---
layout: post
title: Ubuntu声卡独占方法
---

停止Alsa-util
<pre><code>$ sudo /etc/init.d/alsa-utils stop</code></pre>
编辑配置文件
<pre><code>$ sudo gedit /var/lib/alsa/asound.state </code></pre>
将如下内容添加至文件顶部
<pre><code># This text should be added to the beginning of
# /var/lib/alsa/asound.state. You only need to add
# it once -- it is saved across reboots.
pcm.asymed {
type asym
playback.pcm dmix
capture.pcm dsnoop
}
pcm.default {
type plug
slave.pcm asymed
}
pcm.dmix {
type dmix
ipc_key 5678293
ipc_key_add_uid yes
slave {
pcm 'hw:0,0'
period_time 0
period_size 128
buffer_size 2048
format S16_LE
rate 48000
}
}
pcm.dsnoop {
type dsnoop
ipc_key 5778293
ipc_key_add_uid yes
slave {
pcm 'hw:0,0'
period_time 0
period_size 128
buffer_size 2048
format S16_LE
rate 48000
}
}</code></pre>
重新启动声音服务
<pre><code>$ sudo /etc/init.d/alsa-utils start</code></pre>
点击Preferences->Sound菜单，将标签Device里的所有音效全部设置为ALSA，重启电脑。
更改Pidgin音效为ESD方式，这下边听歌边IM都没问题了。
