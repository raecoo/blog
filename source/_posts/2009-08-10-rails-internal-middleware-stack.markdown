---
layout: post
title: Rails Internal Middleware Stack
---

Rails Internal Middleware Stack, see more pls run the "rake middleware" in the project directory.

Rack::Lock
# Sets env["rack.multithread"] flag to true and wraps the application within a Mutex.
ActionController::Failsafe
# Returns HTTP Status 500 to the client if an exception gets raised while dispatching.
ActiveRecord::QueryCache
# Enable the Active Record query cache.
ActionController::Session::CookieStore
# Uses the cookie based session store.
ActionController::Session::MemCacheStore
# Uses the memcached based session store.
ActiveRecord::SessionStore
# Uses the database based session store.
Rack::MethodOverride
# Sets HTTP method based on _method parameter or env["HTTP_X_HTTP_METHOD_OVERRIDE"].
Rack::Head
# Discards the response body if the client sends a HEAD request.
