---
layout: post
title: 基于Sinatra的Http认证
---

收集一些Sinatra的Http Basic认证程序

 * <a href="http://www.gittr.com/index.php/archive/sinatra-basic-authentication-selectively-applied/">Sinatra Basic Authentication – Selectively Applied</a>
   You’ll find similar DIY implementations in many sinatra projects (e.g. sinatra-wiki, ...)

 * <a href="http://github.com/sbfaulkner/sinatra_authentication">sbfaulkner / sinatra_authentication</a>
   Like DIY, but uses Rack::Auth in a nice helper. Easy to use for models classes.

 * <a href="http://github.com/blindgaenger/sinatra-auth">blindgaenger / sinatra-auth</a> « Yep, this project!
   Adds Rack::Auth as middleware and checks protected routes before dispatching to sinatra.

 * <a href="http://github.com/maxjustus/sinatra-authentication">maxjustus / sinatra-authentication</a>
   If you need session based authentication using DataMapper, this is for you!

 * <a href="http://sinatra.lighthouseapp.com/projects/9779/tickets/16-patch-http-authentication">Sinatra Lighthouse [PATCH] HTTP Authentication</a>
   But actually I really hope any HTTP authentication will become an integrated part of sinatra!

* <a href="http://github.com/blindgaenger/sinatra-auth/tree/master">sinatra-auth</a>
  use the basic HTTP authentication of rack in your sinatra application
