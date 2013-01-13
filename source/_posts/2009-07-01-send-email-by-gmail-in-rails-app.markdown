---
layout: post
title: 在Rails程序中使用Gmail发送邮件
---

Gmail发送邮件是需要TLS的支持才可以的，ActionMailer默认不支持TLS，需要添加一个插件来实现此功能
<pre><code>./script/plugin install git://github.com/collectiveidea/action_mailer_optional_tls.git</code></pre>
添加Email设置的选项
touch config/initializers/email_setting.rb
vim config/initializers/email_setting.rb
添加如下内容即可
<pre><code>ActionMailer::Base.smtp_settings = {
    :tls => true,
    :address => "smtp.gmail.com",
    :port => "587",
    :domain => "YOURDOMAIN",
    :authentication => :plain,
    :user_name => "GOOGLEUSERNAME",
    :password => "GOOGLEPASSWORD"
}</code></pre>
