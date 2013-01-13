---
layout: post
title: 基于gitosis创建新的版本仓库
---

在此以添加一个名为VOD的版本库为例:
 
1. 编辑gitosis.conf, 为VOD版本库添加兩个可操作的成员, 并提交修改的配置文件.
<pre><code>[group team]
members = raecoo peter
writable   = vod
# commit modified
$git commit -a -m "Allow raecoo & peter write access to vod"
$git push</code></pre>
2. 创建并初始化VOD版本库.
<pre><code>mkdir vod
$cd vod
$git init
$git remote add origin git@YOUR_SERVER_HOSTNAME:vod.git
# add and commit files
$git push origin master:refs/heads/master</code></pre>

Reference: <a href="http://scie.nti.st/2007/11/14/hosting-git-repositories-the-easy-and-secure-way">http://scie.nti.st/2007/11/14/hosting-git-repositories-the-easy-and-secure-way</a>
