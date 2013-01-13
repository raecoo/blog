---
layout: post
title: need public signing key
---

<pre><code>gpg --keyserver keyserver.ubuntu.com --recv 5AFADBD4AA1C92B0
gpg --export --armor 5AFADBD4AA1C92B0 | sudo apt-key add -</code></pre>
