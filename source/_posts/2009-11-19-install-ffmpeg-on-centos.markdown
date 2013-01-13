---
layout: post
title: 安装FFMpeg
---

FFMPEG是一个开放源代码的跨平台的流媒体解码程序, N多的软件都采用它做为解码核心, 貌似还有一个叫 FFMPEG耻辱名单的玩意, 是指一些个商业公司不遵守FFMPEG的发布协议. 但毕竟是开源产品没有过多的法律保护, 也只能靠自控解决.

FFMPEG的依赖关系比较复杂, 同事曾经自行编译安装未遂, 而后找到一个RPM源, 直接升级安装即可, 不用再为依赖关系和漫长的make过程而头疼. 安装过程如下(CentOS):

1. 创建yum升级源配置文件(/etc/yum.repos.d/dag.repo), 并添加如下内容.
<pre><code>[dag]
name=DAG RPM Repository
baseurl=http://apt.sw.be/redhat/el$releasever/en/$basearch/dag
gpgcheck=1
enabled=1</code></pre>
<!--more-->
2. 导入RPM认证key文件
<pre><code>rpm --import http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt</code></pre>
3. 更新源, 安装FFMPEG
<pre><code>yum update
yum search ffmpeg
yum install ffmpeg ffmpeg-devel ffmpeg-libpostproc mencoder</code></pre>
