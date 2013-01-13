---
layout: post
title: global git config file
---

this is my .gitconfig file content
<pre><code>[user]
  name = Raecoo Cao
  email = raecoo{#}gmail.com
[color]
  diff = auto
  status = auto
  branch = auto
[alias]
  st = status
  rb = svn rebase
  ci = commit -a
  co = checkout</code></pre>
how to generate it? run the follow commands
<pre><code> $ git config --global user.email Your.Email@domain.com
 $ git config --global user.name "Your Real Name"</code></pre>
