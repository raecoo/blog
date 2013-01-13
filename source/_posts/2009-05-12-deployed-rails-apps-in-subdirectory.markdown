---
layout: post
title: 在子目录中部署Rails应用程序
---

今天做测试需要将多个Rails应用程序部署在一个域名下的多个不同的子目录,例如:
<pre><code>http://domain.com/           主应用
http://domain.com/app1    子应用1
http://domain.com/app2    子应用2</code></pre>
测试环境主要通过Nginx+Mongrel+Rails 2.2.2组合.Nginx和Mongrel的安装不在本文讨论范围之内,请自行Google.
<!--more-->
此部署方式的关键在于指定Rails应用的子目录,这在生成mongrel集群配置文件时即可一次性设置,比如:
<pre><code> mongrel_rails cluster::configure -e development -p 6000 -N 2 -c /home/your/app/path -a 127.0.0.1 --prefix /main</code></pre>
生成的文件内容如下:
<pre><code>---
address: 127.0.0.1
prefix: /main
log_file: log/mongrel.log
port: "6000"
cwd: /home/raecoo/examples/app
environment: development
pid_file: tmp/pids/mongrel.pid
servers: 2</code></pre>
重点是prefix这个参数,需要注意的此参数需要与Nginx虚拟主机里的转发过滤条件相一致才行,即:
<pre><code>
server {
  .........
  location /main {
    proxy_pass http://sparrow_main_mongrel;
    proxy_redirect  off;
    proxy_set_header  Host        $host;
    proxy_set_header  X-Real-IP   $remote_addr;
    proxy_set_header  X-Forwarded-For  $proxy_add_x_forwarded_for;
  }
 ...........
}</code></pre>
这样基本上就大功告成了,另附一虚拟主机的<a href="http://www.raecoo.com/wp-content/uploads/2009/05/sparrowcom.conf">配置文件</a>以便参考使用.

另: 启动应用会可能会出现如下错误,因项目采用memcached保存session,所以也没太在意如下错误的原因,如有哪位朋友知道可以告知 :)
<pre><code>CGI::Session::CookieStore::TamperedWithCookie</code></pre>
