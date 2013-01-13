---
layout: post
title: 修改TextMate加载文件夹的配置
---

修改TextMate的文件加载过滤设置.
open TextMate -> CMD+, -> Advanced -> Folder References -> Folder Pattern,填入新的正则表达式即可
<pre><code># modify version 2
!.*/(\.[^/]*|vendor/rails|vendor/.*/test|log|doc|CVS|_darcs|_MTN|\{arch\}|blib|.*~\.nib|.*\.(framework|app|pbproj|pbxproj|xcode(proj)?|bundle))$
# modify version 1
!.*/(\.[^/]*|vendor|CVS|_darcs|_MTN|\{arch\}|blib|.*~\.nib|.*\.(framework|app|pbproj|pbxproj|xcode(proj)?|bundle))$
# default
!.*/(\.[^/]*|CVS|_darcs|_MTN|\{arch\}|blib|.*~\.nib|.*\.(framework|app|pbproj|pbxproj|xcode(proj)?|bundle))$</code></pre>
参考:
<a href="http://www.colorsofmysea.com/2009/04/folder-pattern-for-textmate/">folder-pattern-for-textmate</a>
<a href="http://railspikes.com/2007/11/13/textmate-rails-remove-vendor-files">textmate-rails-remove-vendor-files</a>
