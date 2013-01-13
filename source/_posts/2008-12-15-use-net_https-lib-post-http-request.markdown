---
layout: post
title: 使用net/http发送请求
---

下面是使用Ruby通过Http请求读取del.icio.us的一个示例.
<pre><code>require 'net/https'
require "rexml/document"
username = "" # your del.icio.us username
password =  "" # your del.icio.us password
resp = href = "";
begin
  http = Net::HTTP.new("api.del.icio.us", 443)
  http.use_ssl = true
  http.start do |http|
    req = Net::HTTP::Get.new("/v1/tags/get", {"User-Agent" =>
        "raecoo.com"})
    req.basic_auth(username, password)
    response = http.request(req)
    resp = response.body
  end
  #  XML Document
  doc = REXML::Document.new(resp)
  # iterate over each element
  doc.root.elements.each do |elem|
    print elem.attributes['tag']  + " -> " +
	elem.attributes['count'] + "\n"
  end
rescue SocketError
  raise "Host " + host + " nicht erreichbar"
rescue REXML::ParseException => e
  print "error parsing XML " + e.to_s
end
</code></pre>
