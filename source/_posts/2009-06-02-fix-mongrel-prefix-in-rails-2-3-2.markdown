---
layout: post
title: 解决Rails 2.3.2中不识别mongrel prefix参数的方法
---

采用mongrel部署应用到子目录里会用到prefix这个选项,但此选项目前在Rails 2.3.2会出现如下错误
<pre><code> uninitialized constant ActionController::AbstractRequest (NameError)</code></pre>
这是因为Rails内部改变了类名导致的,手工Hack一下,在environment.rb里添加如下代码
<pre><code>Rails::Initializer.run do |config|
 ...
 config.action_controller.relative_url_root = "/path"
 ...
end</code></pre>
在config/initializers目录下新建一个action_controller.rb并填入以下代码(当然也可以直接添加在environment.rb中)
<pre><code>module ActionController
  class AbstractRequest < ActionController::Request
    def self.relative_url_root=(path)
      ActionController::Base.relative_url_root=(path)
    end
    def self.relative_url_root
      ActionController::Base.relative_url_root
    end
  end
end</code></pre>
重启应用就O了
