---
layout: post
title: 使用Unit Png Fix 解决IE6 下PNG图片不透明问题
---

IE6 不支持PNG格式的图片透明,以前也用过一些方法解决,但或多或少都需要写CSS,再加载一堆文件,很麻烦,无意间发现 <a href="http://http://labs.unitinteractive.com/unitpngfix.php">Unit Png Fix</a> 很不错,只需要添加一个JS和一个很小的图片即可解决问题.

unitpngfix.js默认将从images目录查找名为clear.gif的图片,可根据情况进行修改
