---
layout: post
title: install RMagick on Debian
---

Run follows command in the shell
<pre><code>sudo apt-get install imagemagick librmagick-ruby libmagick9-dev
sudo gem install rmagick</code></pre>
Check the installation results
<pre><code>irb -rubygems -r RMagick
puts Magick::Long_version </code></pre>
