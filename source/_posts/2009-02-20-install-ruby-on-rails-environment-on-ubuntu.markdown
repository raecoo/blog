---
layout: post
title: install ruby on rails environment on ubuntu
---

install ruby on rails on ubuntu very easy, follow me:
first,install ruby, rmagick and releated lib
<pre><code>sudo apt-get install libssl0.9.8 libssl0.9.8-dbg libssl-dev
sudo apt-get install ruby libzlib-ruby rdoc ri irb ruby1.8-dev
sudo apt-get install libopenssl-ruby libgd-ruby1.8 imagemagick
sudo apt-get install libmagick9-dev ruby1.8-dev</code></pre>
next,install gem,the apt source rubygems too old,so i like make it by self
<pre><code>wget http://rubyforge.org/frs/download.php/45905/rubygems-1.3.1.tgz
tar zxvf rubygems-1.3.1.tgz; cd rubygems-1.3.1
sudo ruby setup.rb</code></pre>
ok,let's install all of the common gems
<pre><code>sudo gem install rmagick
sudo gem install rails merb
sudo gem install ....</code></pre>
<!--more-->the other way
<pre><code>apt-get -y install build-essential zlib1g zlib1g-dev libxml2 libxml2-dev libxslt-dev sqlite3 libsqlite3-dev locate git-core
apt-get -y install curl wget
apt-get -y install libmagick9-dev
apt-get -y install ruby1.8-dev ruby1.8 ri1.8 rdoc1.8 irb1.8 libreadline-ruby1.8 libruby1.8 libopenssl-ruby
ln -s /usr/bin/ruby1.8 /usr/bin/ruby
ln -s /usr/bin/rdoc1.8 /usr/bin/rdoc
ln -s /usr/bin/irb1.8 /usr/bin/irb
ln -s /usr/bin/ri1.8 /usr/bin/ri
curl http://de.mirror.rubyforge.org/rubygems/rubygems-1.3.1.tgz | tar -xzv
cd rubygems-1.3.1 &amp;&amp; ruby setup.rb install
cd .. &amp;&amp; rm -rf rubygems-1.3.1
ln -s /usr/bin/gem1.8 /usr/local/bin/gem
gem sources -a http://gems.github.com # add Github as a gem source, you won't regret it
gem install rake nokogiri hpricot builder cheat daemons json uuid rmagick sqlite3-ruby fastthread rack</code></pre>
