---
layout: post
title: how to use ruby invoke remote url
---

调用远程URL接口的通用方法,临时封装的,还不完善,仅供参考,相信封装完善后将是一个不错的Libary,其实RESTFul的远程也类似这样,但Rails自己封装的肯定比这个要成熟的多,抽空也Copy一个出来,记录在此
<pre><code>
require 'net/http'
require 'net/https'
require "singleton"
require "erb"
def	invoke_remote
	RemoteHttp.instance
end
class RemoteHttp
	include Singleton
	def call(host,url,request_type,params={})
		http = Net::HTTP.new(host)
		response, data = http.get(host+url, nil)
		puts '----------------------------------------------------'
		puts response
		puts '----------------------------------------------------'
		puts data
		puts '----------------------------------------------------'
	end
end
invoke_remote.call('http://www.p1.cn','/raecoo','',{})
</code></pre>
