---
layout: post
title: Ruby数值常用操作方法
---

Ruby中常用的数值操作方法

# 2进制,8进制,16进制向数值型转换
Example:
<pre><code>p 0b10000     #=&gt; 16
p 020     #=&gt; 16
p 0×10    #=&gt; 16</code></pre>

# 数值型向2进制,8进制,16进制转换
Example:
<pre><code>s = 255.to_s(2)     #=&gt; “11111111″
s = “%b”  % 255     #=&gt; “11111111″
s = sprintf(”%o”, 255)     #=&gt; “377″
s = format(”%x”, 255)     #=&gt; “ff”</code></pre>

# 商和余数的计算
Example: i = 10
<pre><code>p i % 3     #=&gt; 1
p i.divmod(3)     #=&gt; [3, 1]</code></pre>

<!--more--># 绝对值的计算
Example: i = -5
<pre><code>p i.abs     #=&gt; 5
i=100
p i.abs     #=&gt; 100</code></pre>

# 返回比float大的最小整数
Example: f = 3.4
<pre><code>p f.ceil     #=&gt; 4</code></pre>

# 返回比float小的最大整数
Example: f = 3.4
<pre><code>p f.truncate     #=&gt; 3</code></pre>

# 四舍五入到一个整数
Example: f1 = 3.4
<pre><code>f2 = 3.5
p f1.round     #=&gt; 3
p f2.round     #=&gt; 4</code></pre>

# 返回float截掉小数点后的整数
Example: f1 = 3.48
<pre><code>f2 = 3.48
p f1.to_i    #=&gt; 3
p f2.to_i    #=&gt; 3</code></pre>

# 乱数
Example:
<pre><code>p rand(100)     #=&gt; 17</code></pre>
