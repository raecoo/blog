---
layout: post
title: Rails无法正常产生日志的解决方法
---

昨天部署一个应用时发现不能够正常产生log文件,环境为Nginx + Passenger,后来发现原因很简单,应用所在目录的owner是root用户,改为非root用户即可恢复正常,看起来随意使用root确实不是一个好习惯,以后要注意.
