---
layout: post
title: 在DataMapper中应用内存表
---

DataMapper在多数据库连接,单表继承以及对遗留数据库的支持上做的是相当不错的,今天用到了内存表的设置,感觉方式很清晰,赞一个先~
在init.rb里加上这个语句,声明一个使用in_memory的Adapter
<pre><code>DataMapper.setup(:in_memory, :adapter => 'in_memory')</code></pre>
在需要以内存表方式存储的Model里加上如下语句,促使在执行相关Migrate时做对应的处理
<pre><code>class Online
  include DataMapper::Resource
  # Use in_memory adapter
  def self.default_repository_name;:in_memory;end
  def self.auto_migrate_down!(rep);end
  def self.auto_migrate_up!(rep);end
  def self.auto_upgrade!(rep);end
  #
  property :id, Serial
  property :user_id,	Integer,	:nullable=>false
  property :whereis,	String,		:length=>2000
  property :login_at, DateTime
  property :active_at,DateTime
end</code></pre>
就这么简单,DataMapper使用它内置的In-memory适配器来控制这个Model,所以在数据库表清单里是看不到这个表的,但可以直接对其进行操作(CRUD).

<a href="http://datamapper.org/doku.php?id=docs:misc#multiple_data-store_connections">http://datamapper.org/doku.php?id=docs:misc#multiple_data-store_connections</a>
