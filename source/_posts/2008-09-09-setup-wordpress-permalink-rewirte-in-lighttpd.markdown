---
layout: post
title: lighttpd下WordPress的Permalink Rewirte
---

<ol>
	<li>a Wordpress blog installed in the root of your (sub-) domain:
<pre><code>$HTTP["host"] =~ "{yourdomain}" {
var.app  = "{yourdomain}"
accesslog.filename = base + "/logs/" + app + ".access.log"
server.errorlog = base + "/logs/" + app + ".error.log"
load php app
url.rewrite = (
"^/(wp-.+).*/?" =&gt; "$0",
"^/(sitemap.xml)" =&gt; "$0",
"^/(xmlrpc.php)" =&gt; "$0",
"^/(.+)/?$" =&gt; "/index.php/$1"
)
}</code></pre></li>
	<li> a Wordpress blog installed in a subfolder (e.g. /blog/)
<pre><code>$HTTP["host"] =~ "{yourdomain}" {
var.app = "{yourdomain}"
accesslog.filename = base + "/logs/" + app + ".access.log"
server.errorlog = base + "/logs/" + app + ".error.log"
load php app
url.rewrite = (
"^/?$" =&gt; "/blog/index.php",
"^/blog/(wp-.+)$" =&gt; "$0",
"^/blog/xmlrpc.php" =&gt; "$0",
"^/blog/sitemap.xml" =&gt; "$0",
"^/blog/(.+)/?$" =&gt; "/blog/index.php/$1"
)
}</code></pre></li>
	<li><span style="font-family: -webkit-monospace;">may be you can add follow line in config file</span></li>
</ol>
<span style="font-family: -webkit-monospace;">     server.error-handler-404= "/index.php"</span>
