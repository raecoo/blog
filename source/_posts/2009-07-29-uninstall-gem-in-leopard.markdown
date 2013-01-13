---
layout: post
title: 在Leopard 卸载gem安装包
---

Leopard装好后默认带了一些比较老的安装包想要卸载,但提示
<pre><code>ERROR:  While executing gem ... (Gem::InstallError)
    cannot uninstall, check `gem list -d package_name`</code></pre>
google后发现需要指定一下安装路径就可以正常卸载了.
<pre><code>sudo gem uninstall net-ssh -v=1.1.2 --install-dir=/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/lib/ruby/gems/1.8/</code></pre>
