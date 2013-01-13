---
layout: post
title: Mechanize使用实践
---

周末无事,就写了个小蜘蛛,去抓了一些google music的文件下来,目的就是试试mechanize这个东东的用法,感觉很容易上手,关键是速度不错.代码也超级简单,不过只能下载一定数量的mp3, google会对貌似蜘蛛的程序进行限制,添加一个验证码的确认.
<pre><code>
#!/usr/bin/env ruby
require 'rubygems'
require 'nokogiri'
require 'mechanize'
require 'cgi'
a = WWW::Mechanize.new { |agent|
  agent.user_agent_alias = 'Mac Safari'
}
target_page = a.get('http://www.google.cn/music/search?q=%E5%BC%A0%E6%82%AC&cat=song')
doc = Nokogiri::HTML(target_page.parser.to_s)
nodes = doc.xpath('//div[@class="results"]/table[@id="song_list"]/tr')
song_ids = []
puts "-- found #{nodes.size} nodes"
nodes.each { |song| song_ids << (song.attribute('id').to_s.gsub('row','')) }
song_ids.each do |sid|
  target = "http://www.google.cn/music/top100/musicdownload\?id=#{sid}"
  puts "--- Target url --- =>  #{target}"
  system("echo --- #{target} >> down_music.txt")
  down_base = a.get(target)
  down_base.links_with(:href => %r{/music/}).each do |link|
    next if link.href !~ %r{/music/}
    down = CGI.unescape(link.href.gsub('/music/top100/url?q=','').split('&').first)
    puts down
    system("echo === #{down} >> down_music.txt")
    system("curl -O #{down}")
  end
end
</code></pre>
