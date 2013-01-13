---
layout: post
title: Scrot截图工具
---

Ubuntu自带的那个截图工具实在是不好用,Google了一下发现有人推荐Scrot这个小玩意,试了一下感觉相当爽!
特点,小巧,实用,可以点击截图,可以选取截图,速度非常快!
<pre><code>sudo apt-get install scrot
sudo gedit /usr/share/applications/scrot.desktop
[Desktop Entry]
Name=Scrot
Comment=屏幕截图
Exec=/usr/bin/scrot -s -b -e 'mv $f ~/Document/snapshoots/'
Icon=
Terminal=false
Type=Application
Categories=Application;Graphics;</code></pre>
