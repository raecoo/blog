---
layout: post
title: 开启Safari的Web调试工具
---

在终端内输入如下内容即可:
<pre><code>$defaults write com.apple.Safari  WebKitDeveloperExtras -bool true</code></pre>
重启Safari, 样子和Chrome的几乎一样, 看赶来还不错.

UPDATE: 
强制以标签打开网页
<pre><code>$defaults write com.apple.Safari TargetedClicksCreateTabs -bool true</code></pre>
让Finder支持剪切操作
<pre><code>$defaults write com.apple.finder AllowCutForItems 1</code></pre>
