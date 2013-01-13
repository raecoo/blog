---
layout: post
title: http authentication
---

some information about http authentication :
--
As for authentication, the HTTP protocol includes the basic access authentication and the digest access authentication protocols, which allow access to a Web page only when the user has provided the correct username and password. If the server requires such credential for granting access to a Web page, the browser requests them to the user; once obtained, the browser stores and uses them also for accessing subsequent pages, without requiring the user to provide them again. From the point of view of the user, the effect is the same as if cookies were used: username and password are only requested once, and from that point on the user is given access to the site. In the basic access authentication protocol, a combination of username and password is sent to the server in every browser request. This means that someone listening in on this traffic can simply read this information and store for later use. This problem is overcome in the digest access authentication protocol, in which the username and password are encrypted using a random nonce created by the server.

see more <a href="http://en.wikipedia.org/wiki/Basic_access_authentication" target='_blank'>http://en.wikipedia.org/wiki/Basic_access_authentication</a>
