---
layout: post
title: Rails Model 验证固定电话与手机
---

<pre><code>\d{3,4}[-]\d{7,8}[-]\d{0,1} 固定电话
((\d{3}\-))?13[0-9]\d{8}|15[89]\d{8} 手机</code></pre>

<pre><code>  validates_format_of :phone,
    :with => /^(\d{3,4}[-]\d{7,8})|(((\d{3}\-))?13[0-9]\d{8}|15[89]\d{8})$/,
    :allow_blank  => true</code></pre>
