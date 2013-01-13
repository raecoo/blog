---
layout: post
title: 自定义常用的Shell命令
---

<pre><code>export PS1="[\u@\h:\w]$"

alias ll="ls -ls"
alias la="ls -al"

alias ss="script/server"
alias pss="RAILS_ENV=production script/server"
alias sc="script/console"
alias psc="RAILS_ENV=production script/console"

alias get="git pull"
alias put="git push"
alias pt='touch tmp/restart.txt'

function p
{
  cd "/Users/raecoo/projects/$@"
}

function log
{
  p "$@"
  tail -f -n200 "log/development.log"
}

function ci
{
  git ci -a -m "$@"
}

function ssp
{
  script/server -p "$@"
}</code></pre>
