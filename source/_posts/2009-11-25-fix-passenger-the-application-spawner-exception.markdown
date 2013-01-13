---
layout: post
title: 解决Passenger的Unexpected end-of- file detected异常
---

今天在启动一个项目时出现了如下错误信息:
<pre><code>Passenger encountered the following error:

The application spawner server exited unexpectedly: Unexpected end-of-
file detected.

Exception class:
    PhusionPassenger::Railz::ApplicationSpawner::Error 
</code></pre>

运行环境: Apache + Passenger(2.2.7) + REE 1.8.7
解决方法: 安装项目依赖的gem包, 如仍有异常请尝试卸载并重新安装依赖gem.
