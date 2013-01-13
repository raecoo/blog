---
layout: post
title: China Region list
---

做项目时总会用到地区列表,包含省,市,区以及上下级关系,今天整理出来一份放在了github上,以便需要的人使用.共提供了三种格式,xml,csv,sql应该能够满足绝大多数情况. :)
<pre><code>git clone git://github.com/raecoo/china-regions.git</code></pre>
顺便贴一小段整理时用到的ruby代码.
<!--more-->
<pre><code>namespace :location do
  desc "build index"
  task :index => :environment do
    name_path = Hash.new { |h, k| h[k] = []}
    ids_path = Hash.new { |h, k| h[k] = []}
    split = '|'
    Location.all.each do |l|
      l.name_path = calculate(name_path, l, :name).join(split)
      l.ids_path  = calculate(ids_path, l, :id).join(split)
      puts "-id => #{l.id} -name_path => #{l.name_path} -ids_path => #{ids_path}"
      l.save
    end
    name_path = nil
    ids_path  = nil
  end

  def calculate(cache, location, attribute)
    return cache[location.id] unless cache[location.id].empty?
    parent = location
    while parent
      cache[location.id].insert(0,parent.send(attribute))
      parent = parent.parent
    end
    return cache[location.id]
  end
end</code></pre>
