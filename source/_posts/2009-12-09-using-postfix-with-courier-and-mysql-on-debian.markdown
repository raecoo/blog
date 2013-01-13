---
layout: post
title: 使用Postfix, Courier及MySql构建自已的邮件服务器
---

本文将介绍如何在Ubuntu上运行Postfix邮件系统, 使用Courier提供IMAP/POP3(IMAPS and POP3S)服务, 并将虚拟域和用户数据保存于MySql中.

<strong>1. 安装必须的软件包</strong>
<pre><code>apt-get install postfix postfix-mysql postfix-doc mysql-client mysql-server courier-authdaemon \
        courier-authlib-mysql courier-pop courier-pop-ssl courier-imap courier-imap-ssl \
        libsasl2-2 libsasl2-modules libsasl2-modules-sql sasl2-bin libpam-mysql openssl</code></pre>
安装过程中需要输入MySql的root密码, 在选择邮件服务器类型时选择"Internet Site", 在输入system mail name
时请输入一个完整的域名并指向服务器的IP地址.
<!--more-->
<strong>2. 设置虚拟域及用户</strong>
<pre><code>$mysql -uroot -p
mysql>create database mail_system;
mysql>use mail_system;
mysql>GRANT ALL ON mail_system.* TO 'mail_admin'@'localhost' IDENTIFIED BY 'mail_admin_password';
mysql>FLUSH PRIVILEGES;</code></pre>
创建虚拟域数据表
<pre><code>mysql>CREATE TABLE domains (domain varchar(50) NOT NULL, PRIMARY KEY (domain) );</code></pre>
创建虚拟用户数据表
<pre><code>mysql>CREATE TABLE users (email varchar(80) NOT NULL, password varchar(20) NOT NULL,
  PRIMARY KEY (email) );</code></pre>
创建邮件转发数据表(可选项)
<pre><code>mysql>CREATE TABLE forwardings (source varchar(80) NOT NULL, destination TEXT NOT NULL,
  PRIMARY KEY (source) );</code></pre>
创建Transport数据表(可选项)
<pre><code>mysql>CREATE TABLE transport (domain varchar(128) NOT NULL default '', transport varchar(128) NOT NULL default '', UNIQUE KEY domain (domain));</code></pre>
绑定MySql
<pre><code>$vim /etc/mysql/my.cnf
bind-address = 127.0.0.1</code></pre>
重启MySql
<pre><code>$/etc/init.d/mysql restart</code></pre>

<strong>3. 设置Postfix使其支持MySql</strong>

创建虚拟域配置文件
<pre><code>$vim /etc/postfix/mysql-virtual_domains.cf
user = mail_admin
password = mail_admin_password
dbname = mail_system
query = SELECT domain AS virtual FROM domains WHERE domain='%s'
hosts = 127.0.0.1</code></pre>
创建虚拟收件箱配置文件
<pre><code>$vim /etc/postfix/mysql-virtual_mailboxes.cf
user = mail_admin
password = mail_admin_password
dbname = mail_system
query = SELECT CONCAT(SUBSTRING_INDEX(email,'@',-1),'/',SUBSTRING_INDEX(email,'@',1),'/')
        FROM users WHERE email='%s'
hosts = 127.0.0.1</code></pre>
创建虚拟转发配置文件(可选项)
<pre><code>$/etc/postfix/mysql-virtual_forwardings.cf
user = mail_admin
password = mail_admin_password
dbname = mail_system
query = SELECT destination FROM forwardings WHERE source='%s'
hosts = 127.0.0.1</code></pre>
创建虚拟邮件关系配置文件(可选项)
<pre><code>$vim /etc/postfix/mysql-virtual_email2email.cf
user = mail_admin
password = mail_admin_password
dbname = mail_system
query = SELECT email FROM users WHERE email='%s'
hosts = 127.0.0.1</code></pre>
设置文件权限与属主信息
<pre><code>$chmod o= /etc/postfix/mysql-virtual_*.cf
$chgrp postfix /etc/postfix/mysql-virtual_*.cf</code></pre>
接下来, 创建用来处理邮件的用户和组, 所有邮件将保存于此用户的HOME目录,并以虚拟域独立保存
<pre><code>$groupadd -g 5000 vmail
$useradd -g vmail -u 5000 vmail -d /home/vmail -m</code></pre>
修改Postfix的配置文件如下:
<pre><code>myhostname = mail.raecoo.com
mydestination = mail.raecoo.com, localhost, localhost.localdomain
message_size_limit = 30720000
virtual_alias_domains = 
virtual_alias_maps = proxy:mysql:/etc/postfix/mysql-virtual_forwardings.cf, mysql:/etc/postfix/mysql-virtual_email2email.cf
virtual_mailbox_domains = proxy:mysql:/etc/postfix/mysql-virtual_domains.cf
virtual_mailbox_maps = proxy:mysql:/etc/postfix/mysql-virtual_mailboxes.cf
virtual_mailbox_base = /home/vmail
virtual_uid_maps = static:5000
virtual_gid_maps = static:5000
smtpd_sasl_auth_enable = yes
broken_sasl_auth_clients = yes
smtpd_sasl_authenticated_header = yes
smtpd_recipient_restrictions = permit_mynetworks, permit_sasl_authenticated,reject_unauth_destination
smtpd_use_tls = yes
smtpd_tls_cert_file = /etc/postfix/smtpd.cert
smtpd_tls_key_file = /etc/postfix/smtpd.key
virtual_create_maildirsize = yes
virtual_maildir_extended = yes
proxy_read_maps = $local_recipient_maps $mydestination $virtual_alias_maps $virtual_alias_domains $virtual_mailbox_maps $virtual_mailbox_domains $relay_recipient_maps $relay_domains $canonical_maps $sender_canonical_maps $recipient_canonical_maps $relocated_maps $transport_maps $mynetworks $virtual_mailbox_limit_maps</code></pre>

<strong>为Postfix创建SSL证书</strong>
<pre><code>$ cd /etc/postfix
$openssl req -new -outform PEM -out smtpd.cert -newkey rsa:2048 -nodes -keyout smtpd.key
        -keyform PEM -days 365 -x509</code></pre>
一路回车或是将信息填写完整, 再设置一下证书的权限
<pre><code>$chmod o= /etc/postfix/smtpd.key</code></pre>

<strong>4. 设置Saslauthd服务使其支持MySql</strong>
<pre><code>$mkdir -p /var/spool/postfix/var/run/saslauthd
$vim /etc/default/saslauthd
#更改START和OPTIONS为如下所示
START=yes
OPTIONS="-c -m /var/spool/postfix/var/run/saslauthd -r"</code></pre>
创建或编辑/etc/pam.d/smtp, 并添加如下内容(注意是auth和account共两行)
<pre><code>auth    required   pam_mysql.so user=mail_admin passwd=mail_admin_password host=127.0.0.1
        db=mail table=users usercolumn=email passwdcolumn=password crypt=1
account sufficient pam_mysql.so user=mail_admin passwd=mail_admin_password host=127.0.0.1
        db=mail table=users usercolumn=email passwdcolumn=password crypt=1</code></pre>
创建或编辑/etc/postfix/sasl/smtpd.conf
<pre><code>$vim /etc/postfix/sasl/smtpd.conf
pwcheck_method: saslauthd
mech_list: plain login
allow_plaintext: true
auxprop_plugin: mysql
sql_hostnames: 127.0.0.1
sql_user: mail_admin
sql_passwd: mail_admin_password
sql_database: mail
sql_select: select password from users where email = '%u'</code></pre>
添加Postfix用户至Sasl组并重启服务
<pre><code>$/etc/init.d/postfix restart
$/etc/init.d/saslauthd restart</code></pre>

<strong>5. 设置Courier使其支持MySql</strong>
编辑/etc/courier/authdaemonrc文件修改authmodulelist选项值为authmysql
<pre><code>....
authmodulelist="authmysql"
....</code></pre>
编辑/etc/courier/authmysqlrc文件如下
<pre><code>MYSQL_SERVER localhost
MYSQL_USERNAME mail_admin
MYSQL_PASSWORD mail_admin_password
MYSQL_PORT 0
MYSQL_DATABASE mail
MYSQL_USER_TABLE users
MYSQL_CRYPT_PWFIELD password
MYSQL_UID_FIELD 5000
MYSQL_GID_FIELD 5000
MYSQL_LOGIN_FIELD email
MYSQL_HOME_FIELD "/home/vmail"
MYSQL_MAILDIR_FIELD CONCAT(SUBSTRING_INDEX(email,'@',-1),'/',SUBSTRING_INDEX(email,'@',1),'/')</code></pre>
删除Courier创建的证书
<pre><code>$rm -f /etc/courier/imapd.pem
$rm -f /etc/courier/pop3d.pem</code></pre>
分别编辑/etc/courier/imapd.cnf和/etc/courier/pop3d.cnf, 将其中的CN=localhost选项修改为上述中提到的system mail name, 其他选项可以根据需要自行修改, 最后重新生成Courier证书并重启服务
<pre><code>$cd /etc/courier
$mkimapdcert
$mkpop3dcert
$/etc/init.d/courier-authdaemon restart
$/etc/init.d/courier-imap restart
$/etc/init.d/courier-imap-ssl restart
$/etc/init.d/courier-pop restart
$/etc/init.d/courier-pop-ssl restart</code></pre>
这时就可以用telnet来测试一下POP3服务是否正常工作
<pre><code>$telnet localhost pop3
#你将看到如下字样
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
+OK Hello there.</code></pre>

<strong>6. 设置Email别名</strong>
编辑别名配置文件
$vim /etc/aliases
postmaster: root
root: post@raecoo.com
更新文件并重启服务
<pre><code>$newaliases
$/etc/init.d/postfix restart</code></pre>

<strong>7. 测试Postfix安装结果</strong>
<pre><code>$telnet localhost 25
#连接后输入
ehlo localhost
#将看到如下信息
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
220 mail.raecoo.com ESMTP Postfix
ehlo localhost
250-archimedes.palegray.net
250-PIPELINING
250-SIZE 30720000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH CRAM-MD5 NTLM PLAIN LOGIN DIGEST-MD5
250-AUTH=CRAM-MD5 NTLM PLAIN LOGIN DIGEST-MD5
250-ENHANCEDSTATUSCODES
250-8BITMIME
250 DSN</code></pre>

<strong>8. 最后就是添加虚拟域和用户数据了</strong>
<pre><code>$mysql -u root -p
mysql>use mail_system;
mysql>INSERT INTO domains (domain) VALUES ('raecoo.com');
mysql>INSERT INTO users (email, password) VALUES ('sales@raecoo.com', ENCRYPT('password'));</code></pre>

现在来测试一下邮件发送
<pre><code>#安装一个命令行的邮件发送工具
apt-get install mailx
echo "email body" > /tmp/email_test.txt
mailx -s "email subject" sales@raecoo.com < /tmp/email_test.txt</code></pre>
嗯,现在就可以用客户端连接POP3邮箱进行邮件查收了.

这里有一个需要注意的地方就是, 当新创建一个虚拟用户后,该用户收件箱对应的文件夹并不会自动创建. 解决这个问题的方法就是在创建用户后先向此用户发送一个Say Hello的邮件.
还有就是虚拟域的文件夹也是需要提前创建好的, 否则在用户使用POP3登录认证时会发生找不到文件目录的错误.
例如添加了虚拟域raecoo.com, 那就需要在/home/vmail下创建一个名为raecoo.com的目录
References:
http://www.howtoforge.com/virtual-users-domains-postfix-courier-mysql-squirrelmail-ubuntu8.10
https://help.ubuntu.com/community/PostfixBasicSetupHowto
https://help.ubuntu.com/community/Postfix
