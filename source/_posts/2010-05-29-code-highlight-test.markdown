---
layout: default
title: Code Highlight Test
---

{% highlight ruby linenos %}
 mkdir /opt
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
 make install
{% endhighlight %}