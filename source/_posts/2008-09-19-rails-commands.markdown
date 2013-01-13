---
layout: post
title: rails commands
---

rails command list
# rake db:fixtures:load
#   # 载入fixtures到当前环境的数据库
#   # 载入指定的fixtures使用FIXTURES=x,y
#  rake db:migrate
#  # 迁移数据库通过在db/migrate目录下的脚本.可以指定版本号通过VERSION=x
#  rake db:schema:dump
#  # 创建一个db/schema.rb文件，通过AR能过够支持任何数据库去使用
#  rake db:schema:load
#  # 载入一个schema.rb文件进数据库
#  rake db:sessions:clear
#  # 清空sessions表
<!--more-->
#  rake db:sessions:create
#  # 用CGI::Session::ActiveRecordStore创建一个sessions表为用户
#  rake db:structure:dump
#  # 导出数据库结构为一个SQL文件
#  rake db:test:clone
#  # 重新创建一个测试数据库从当前环境数据库中
#  rake db:test:clone_structure
#  # 重新创建测试数据库从开发模式数据库
#  rake db:test:prepare
#  # 准备测试数据库并在入schema
#  rake db:test:purge
#  # 清空测试数据库
#  rake doc:app
#  # 创建HTML文件的API Documentation
#  rake doc:clobber_app
#  # 删除Documentation
#  rake doc:clobber_plugins
#  # 删除 plugin Documentation
#  rake doc:clobber_rails
#  # 删除Documentation
#  rake doc:plugins
#  # 产生Documation为所有安装的plugins
#  rake doc:rails
#  # 创建HTML文件的API Documentation
#  rake doc:reapp
#  # 强制重新创建HTML文件的API Documentation
#  rake doc:rerails
#  # 强制重新创建HTML文件的API Documentation
#  rake log:clear
#  # 清空目录log/下的所有日志文件
#  rake rails:freeze:edge
#  # Lock this application to latest Edge Rails. Lock a specific revision with REVISION=X
#  rake rails:freeze:gems
#  # Lock this application to the current gems (by unpacking them into vendor/rails)
#  rake rails:unfreeze
#  # Unlock this application from freeze of gems or edge and return to a fluid use of system gems
#  rake rails:update
#  # Update both scripts and public/javascripts from Rails
#  rake rails:update:javascripts
#  # Update your javascripts from your current rails install
#  rake rails:update:scripts
#  # Add new scripts to the application script/ directory
#  rake stats
#  # Report code statistics (KLOCs, etc) from the application
#  rake test
#  # Test all units and functionals
#  rake test:functionals
#   # Run tests for functionalsdb:test:prepare
#  rake test:integration
#  # Run tests for integrationdb:test:prepare
#  rake test:plugins
#  # Run tests for pluginsenvironment
#  rake test:recent
#  # Run tests for recentdb:test:prepare
#  rake test:uncommitted
#  # Run tests for uncommitteddb:test:prepare
#  rake test:units
#  # Run tests for unitsdb:test:prepare
#  rake tmp:cache:clear
#  # 清空tmp/cache目录下的所有文件
#  rake tmp:clear
#  # 清空session, cache, 和socket文件从tmp/目录
#  rake tmp:create
#  # 为sessions, cache, and sockets创建tmp/目录
#  rake tmp:sessions:clear
#  # 清空所有在tmp/sessions目录下的文件
#  rake tmp:sockets:clear
#  # 清空所有在tmp/sessions 目录下的ruby_sess.* 文件

# script/about
#  # 输出当前环境信息
#  script/breakpointer
#  # 启动断点server
#  script/console
#  # 启动交换式的Rails控制台
#  script/destroy
#  # 删除通过generators创建的文件
#  script/generate
#  # -> generators
#  script/plugin
#  # -> Plugins
#  script/runner
#  # 执行一个任务在rails上下文中
#  script/server
#  # 启动开发模式服务器http://localhost:3000

# ruby script/generate model ModelName
#  ruby script/generate controller ListController show edit
#  ruby script/generate scaffold ModelName ControllerName
#  ruby script/generate migration AddNewTable
#  ruby script/generate plugin PluginName
#  ruby script/generate mailer Notification lost_password signup
#  ruby script/generate web_service ServiceName api_one api_two
#  ruby script/generate integration_test TestName
#  ruby script/generate session_migration
#  可选项:
#  -p, --pretend Run but do not make any changes.
#  -f, --force Overwrite files that already exist.
#  -s, --skip Skip files that already exist.
#  -q, --quiet Suppress normal output.
#  -t, --backtrace Debugging: show backtrace on errors.
#  -h, --help Show this help message.
#  -c, --svn Modify files with subversion. (Note: svn must be in path)
