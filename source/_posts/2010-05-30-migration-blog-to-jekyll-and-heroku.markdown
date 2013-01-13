---
layout: post
title: Migration Blog to Jekyll and Heroku
tags:  [Jekyll, Heroku]
---

周末研究了一下Jekyll这个开源的静态博客生成系统, 感觉棒极了, 一直以来就希望将自己的网站迁移成一个全静态的平台下, 这样一来网站自身对部署环境依赖将进一步减少, 并且可以很方便的部署与备份.

我个人的网站主要是以博客文章发布为主, 并且我不需要流行的在线编辑器, 所以用Jekyll + Disqus + Heroku来部署一个全新的静态网站是我的最佳选择, 更重点的一点是这样的组合甚至不需要花一分钱在主机租用上, 就目前Heroku提供的100M空间对于一个纯静态的网站来说可以说是足够用(其实我写博客的频度比较低).

在这里首先要感谢一下[galeki](http://galeki.com/), 免费让我在他的服务器上寄居了长达一年半的时间, 其次当然是Jekyll的作者[Tom Preston-Werner](http://github.com/mojombo), 谢谢他写了这么棒的程序并开源给大家使用.

随后我会写一篇关于如何利用Jekyll搭建全静态WEB应用的文章. 希望对感兴趣的朋友有所帮助.