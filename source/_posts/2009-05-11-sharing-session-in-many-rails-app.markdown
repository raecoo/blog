---
layout: post
title: 多个Rails应用间共享Session
---

设置共享Session的关键,多个Apps这里的session_key需要一致
<pre><code>config.action_controller.session = {
  :session_key => 'passport_session',
  :secret      => '9e973115bf92789b246b21135a6e5ecce8c1668b9a3dea6b7857af7dd9cae0c9dfabf0c8fc500eaeee260acb1f0620915258bff1f2e10978841ecaced39acdf2'
}
config.action_controller.session_store = :mem_cache_store
</code></pre>
设置Memcached选项
<pre><code>memcache_options = {
   :compression => true,
   :debug => false,
   :namespace => "app-#{RAILS_ENV}",
   :readonly => false,
   :urlencode => false
}
memcache_servers = [ '192.168.1.50:11211' ]
CACHE = MemCache.new(memcache_options)
CACHE.servers = memcache_servers
ActionController::Base.session_options[:cache] = CACHE
# uncomment the follow option when deploy to production envorinment
#ActionController::CgiRequest::DEFAULT_SESSION_OPTIONS.update(:session_domain => ".domain.com")</code></pre>
取消注释掉的请求验证Key
<pre><code>protect_from_forgery  :secret => '361047277e987fb722ce1d36153ad543'</code></pre>
