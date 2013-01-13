---
layout: post
title: Ruby收取Gmail邮件
---

Gmail的POP3需要用SSL方式才能访问, 今天写了段代码才发现,原来Ruby 1.8.6原生的POP3类库并不支持SSL, 换成1.8.7后就可以了, 看来应该把所有环境里的Ruby版本都进行一下升级了.
<pre><code>#!/usr/bin/env ruby
require 'net/pop'
require 'rubygems'
require 'tmail'

begin
  timeout(30) {
    # set SSL for gmail
    Net::POP3.enable_ssl(OpenSSL::SSL::VERIFY_NONE) # raise exception when ruby version < 1.8.7
    Net::POP3.start("pop.gmail.com", 995, "full-email-address", "password") do |pop|   
      unless pop.mails.empty?
        puts "-- size #{pop.mails.size}"
        pop.mails.each do |email|   
          begin   
            puts "-- receiving mail..." 
            m = TMail::Mail.parse(email.pop)
            puts "-- #{m.subject} -> from: #{m.from}"
          rescue Exception => e   
            puts "Error receiving email at " + Time.now.to_s + "::: " + e.message   
          end   
        end   
      end  
    end
  }
rescue Exception => e
  puts "Exception. #{e.message}"
rescue TimeoutError => e
  puts "Timeout Error. #{e.message}"
end</code></pre>
