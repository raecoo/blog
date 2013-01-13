---
layout: post
title: 升级Leopard默认JDK版本至1.6
---

1. 打开  /Application/Utilities/Java Preferences.app
2. 分别在"Java Applet plugin"和"Java Application"中将"Java SE 6 (64bit)"拖动到列表的顶端;
3. 在终端执行以下命令(貌似不执行也可以):
<pre><code> cd /System/Library/Frameworks/JavaVM.framework/Versions
 sudo mv CurrentJDK CurrentJDK.orig</code></pre>
4. java(c) -version 查看版本.

BTW: go to <a href="http://www.eclipse.org/downloads/download.php?file=/eclipse/downloads/drops/R-3.5.1-200909170800/eclipse-SDK-3.5.1-macosx-cocoa-x86_64.tar.gz">here</a> to download Eclipse 64bit for Mac.
