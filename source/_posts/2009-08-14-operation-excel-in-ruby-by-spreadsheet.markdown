---
layout: post
title: Ruby中使用spreadsheet读写Excel
---

install spreadsheet gem first, then
<pre><code>
require 'rubygems'
require 'spreadsheet'
Spreadsheet.client_encoding = 'UTF-8'
xls = Spreadsheet.open '/Users/raecoo/Downloads/region.xls'
sheet = xls.worksheet 0
sheet.each do |row|
  puts row
  puts row[0]
end
</code></pre>
