---
layout: post
title: deploy rails application with git,capistrano
---

如下脚本仅具备最简单的部署操作,如需要其它操作可添加相应Task
<pre><code>default_run_options[:pty] = true
set :application, "demo"
set :repository, "git url is here"
set :scm, "git"
set :scm_passphrase, "scretpwd"
set :branch, "master" # change branch is here
set :deploy_via, :remote_cache
role :web, "192.168.1.24"
role :app, "192.168.1.24"
set :deploy_to, "/path/to/#{application}"
set :user, "root"
set :password, "scretpwd"
after 'deploy:symlink', 'deploy:symlink_cache'
namespace :deploy do
task :symlink_cache, :except =&gt; { :no_release =&gt; true } do
run "/home/yay/delta/ror/branchs/#{application}/ln_files.sh"
end
task :restart do
run "/home/yay/delta/ror/branchs/#{application}/restart.sh"
end
end</code></pre>
