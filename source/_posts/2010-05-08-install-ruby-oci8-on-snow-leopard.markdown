---
layout: post
title: install ruby-oci8 on snow leopard
---

Download ruby-oci8-2.0.4.tar.gz from <a href="http://rubyforge.org/frs/?group_id=256">rubyforge</a>.

Download at least two packages "Instant Client Package - Basic" and "Instant Client Package - SDK" from <a href="http://www.oracle.com/technology/tech/oci/instantclient/index.html">Oracle Technology Network</a>.

<pre><code> mkdir /opt
 mkdir /opt/oracle
 cd /opt/oracle
 unzip path/to/instantclient-basic-OS-VERSION.zip
 unzip path/to/instantclient-sdk-OS-VERSION.zip
 cd path/to/instantclient
 ln -s libclntsh.dylib.10.1 libclntsh.dylib

 ORACLE_HOME=/opt/oracle/instantclient_10_2
 DYLD_LIBRARY_PATH=/opt/oracle/instantclient_10_2
 export PATH=$DYLD_LIBRARY_PATH:$ORACLE_HOME:$PATH

 gzip -dc ruby-oci8-2.0.4.tar.gz | tar xvf -
 cd ruby-oci8-2.0.4
 make
 make install</code></pre>

or install it by gem

<pre><code>env DYLD_LIBRARY_PATH=/opt/oracle/instantclient_10_2/ ARCHFLAGS="-arch x86_64" gem install ruby-oci8</code></pre>
