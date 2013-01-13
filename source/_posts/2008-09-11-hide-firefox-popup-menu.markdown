---
layout: post
title: 隐藏Firefox的右键菜单
---

Firefox的扩展装多了,右键菜单项也在添加,现在我们就来隐藏一些不常用或不用的菜单项.
首先，定位到个人配置文件夹，找到名为 "chrome" 的子文件夹。你需要编辑该文件夹下的 userChrome.css 文件，如果它不存在就新建之。把下面这行加入 userChrome.css 文件，将可以隐藏任何右键菜单选项。
#id1 { display:none !important; }
把 #id1替换为下面的任何一项：(指明每个选项所对应的右键菜单选项,其实就是定义菜单项的CSS样式)
<!--more-->
#context-openlink 	Open Link in New Window
#context-openlinkintab 	Open Link in New Tab
#context-sep-open 	line separator
#context-bookmarklink 	Bookmark This Link...
#context-savelink 	Save Link As...
#context-sendlink 	Send Link...
#context-copyemail 	Copy Email Address
#context-copylink 	Copy Link Location
#context-sep-copylink 	line separator
#context-viewimage 	View Image
#context-copyimage-contents 	Copy Image
#context-copyimage 	Copy Image Location
#context-sep-copyimage 	line separator
#context-saveimage 	Save Image As...
#context-sendimage 	Send Image...
#context-setWallpaper 	Set As Wallpaper...
#context-blockimage 	Block Images from...
#context-back 	Back
#context-forward 	Forward
#context-reload 	Reload
#context-stop 	Stop
#context-sep-stop 	line separator
#context-bookmarkpage 	Bookmark This Page...
#context-savepage 	Save Page As...
#context-sendpage 	Send Page...
#context-sep-viewbgimage 	line separator
#context-viewbgimage 	View Background Image
#context-undo 	Undo
#context-sep-undo 	line separator
#context-cut 	Cut
#context-copy 	Copy
#context-paste 	Paste
#context-delete 	Delete
#context-sep-paste 	line separator
#context-selectall 	Select All
#context-sep-selectall 	line separator
#context-keywordfield 	Add a Keyword for this Search...
#context-searchselect 	Search Web for ...
#frame-sep 	line separator
#frame 	This Frame
#context-sep-properties 	line separator
#context-viewpartialsource-selection 	View Selection Source
#context-viewpartialsource-mathml 	View MathML Source
#context-viewsource 	View Page Source
#context-viewinfo 	View Page Info
#context-metadata 	Properties
#context-sep-bidi 	line separator
#context-bidi-text-direction-toggle 	Switch Text Direction
#context-bidi-page-direction-toggle 	Switch Page Direction
