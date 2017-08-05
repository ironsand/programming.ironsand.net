---
title: Capistrano3でさくらVPSにdeploy
author: 鉄
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=499
categories:
  - 未分類

---
確実に忘れる上にドキュメントが全然見つからない`Capistrano 3`をVPSにDeployする方法のメモ。
  
作業しながら書いてるのでホントに出来るかは書いてる本人もわかりません。

基本的にはRailscastの[&#8220;Deploying to a VPS&#8221;][1]の設定と`Capistrano 3`の組み合わせです。

### 環境

Windows 7
  
Capistrano 3.1.0
  
rails 4.1.0
  
ruby 2.0.0p195 (2013-05-14) [i386-mingw32]
  
Postgresql
  
さくらのVPS (一番安いの)

### git リポジトリ

VPS上にgit repositoryを作成しておいてそこにプロジェクトをpushしときます。
  
場所は `var/git-repos/#{site}.git`。

### Gemfile

<pre class="lang:ruby decode:true " ># Use unicorn as the app server
gem 'unicorn', group: :production

# Use Capistrano for deployment
gem 'capistrano', '~&gt; 3.1'
gem 'capistrano-rails', '~&gt; 1.1'
gem 'capistrano-rbenv', '~&gt; 2.0'
</pre>

### Nginx

`Nginx`の設定ファイルを`config/nginx.conf`に作成。※`#{site}`は適当に置き換える。

<pre class="lang:default decode:true " >upstream unicorn_${site} {
    server unix:/tmp/unicorn.${site}.sock fail_timeout=0;
}

server {
    listen 80;
    server_name ${site}.com;
    access_log /var/log/nginx/${site}.com.access.log;
    error_log /var/log/nginx/${site}.com.error.log info;
    
    root /var/www/${site}.com/current/public;
    
    location ^~ /assets/ {
        gzip_static on;
        expires max;
        add_header Cache-Control public;
    }

    try_files $uri/index.html $uri @unicorn;
    location @unicorn {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        proxy_pass http://unicorn_${site};
    }

    error_page 500 502 503 504 /500.html;
    client_max_body_size 4G;
    keepalive_timeout 10;
}
</pre>

### Postgresql

chefでも使ってインストールしときましょう。

ローカルでもサーバー上でも`user: deployer`, `password: {none}` な設定にして`database.yml`周りの変更をなくしてます。

### Unicorn

Unicorn用の設定を `config/unicorn.rb`に作成する。

<pre class="lang:ruby decode:true " >root = "/var/www/${site}.com/current"
working_directory root
pid "#{root}/tmp/pids/unicorn.pid"
stderr_path "#{root}/log/unicorn.log"
stdout_path "#{root}/log/unicorn.log"

listen "/tmp/unicorn.${site}.sock"
worker_processes 2
timeout 180
</pre>

こっちは起動・停止などの操作用

<pre class="lang:sh decode:true " title="config/unicorn_init.sh" >#!/bin/sh
set -e

# Feel free to change any of the following variables for your app:
TIMEOUT=${TIMEOUT-60}
APP_ROOT=/var/www/${site}.com/current
PID=$APP_ROOT/tmp/pids/unicorn.pid
CMD="cd $APP_ROOT; bundle exec unicorn -D -c $APP_ROOT/config/unicorn.rb -E production"
AS_USER=deployer
set -u

OLD_PIN="$PID.oldbin"

sig () {
  test -s "$PID" && kill -$1 `cat $PID`
}

oldsig () {
  test -s $OLD_PIN && kill -$1 `cat $OLD_PIN`
}

run () {
  if [ "$(id -un)" = "$AS_USER" ]; then
    eval $1
  else
    su -c "$1" - $AS_USER
  fi
}

case "$1" in
start)
  sig 0 && echo &gt;&2 "Already running" && exit 0
  run "$CMD"
  ;;
stop)
  sig QUIT && exit 0
  echo &gt;&2 "Not running"
  ;;
force-stop)
  sig TERM && exit 0
  echo &gt;&2 "Not running"
  ;;
restart|reload)
  sig HUP && echo reloaded OK && exit 0
  echo &gt;&2 "Couldn't reload, starting '$CMD' instead"
  run "$CMD"
  ;;
upgrade)
  if sig USR2 && sleep 2 && sig 0 && oldsig QUIT
  then
    n=$TIMEOUT
    while test -s $OLD_PIN && test $n -ge 0
    do
      printf '.' && sleep 1 && n=$(( $n - 1 ))
    done
    echo

    if test $n -lt 0 && test -s $OLD_PIN
    then
      echo &gt;&2 "$OLD_PIN still exists after $TIMEOUT seconds"
      exit 1
    fi
    exit 0
  fi
  echo &gt;&2 "Couldn't upgrade, starting '$CMD' instead"
  run "$CMD"
  ;;
reopen-logs)
  sig USR1
  ;;
*)
  echo &gt;&2 "Usage: $0 &lt;start|stop|restart|upgrade|force-stop|reopen-logs&gt;"
  exit 1
  ;;
esac</pre>

### Capistrano 初期化

<pre class="lang:sh decode:true " >$ bundle exec cap install</pre>

で以下のファイルが生成される。

    ├── Capfile
    ├── config
    │   ├── deploy
    │   │   ├── production.rb
    │   │   └── staging.rb
    │   └── deploy.rb
    └── lib
        └── capistrano
                └── tasks
    

### Capfile の設定

`rbenv`を使うか`rvm`を使うかなどで適宜変更。うちはsystemインストールした`rbenv`を使うのでこんな感じ。rubyのバージョンが若干古めなのはWindowsのRailsinstallerに合わせてるので。

<pre class="lang:ruby decode:true " title="Capfile" ># Load DSL and Setup Up Stages
require 'capistrano/setup'

# Includes default deployment tasks
require 'capistrano/deploy'

# Includes tasks from other gems included in your Gemfile
#
# For documentation on these, see for example:
#
#   https://github.com/capistrano/rvm
#   https://github.com/capistrano/rbenv
#   https://github.com/capistrano/chruby
#   https://github.com/capistrano/bundler
#   https://github.com/capistrano/rails
#
# require 'capistrano/rvm'
 require 'capistrano/rbenv'
# require 'capistrano/chruby'
 require 'capistrano/bundler'
 require 'capistrano/rails/assets'
 require 'capistrano/rails/migrations'

# config/deploy.rb
set :rbenv_type, :system # or :user, depends on your rbenv setup
set :rbenv_ruby, '2.0.0-p195'
set :rbenv_path, '/usr/local/rbenv'
set :rbenv_prefix, "RBENV_ROOT=#{fetch(:rbenv_path)} RBENV_VERSION=#{fetch(:rbenv_ruby)} #{fetch(:rbenv_path)}/bin/rbenv exec"
set :rbenv_map_bins, %w{rake gem bundle ruby rails}
set :rbenv_roles, :all # default value

# Loads custom tasks from `lib/capistrano/tasks' if you have any defined.
Dir.glob('lib/capistrano/tasks/*.cap').each { |r| import r }</pre>

### deploy.rb の設定

Capistranoの設定。2に比べてリンクするディレクトリの設定とかをやってくれるようになってるので楽です。それに関するドキュメントが少なくてつらい思いをすることを除けばね！

<pre class="lang:ruby decode:true " ># config valid only for Capistrano 3.1
lock '3.1.0'

set :application, '${site}'
set :repo_url, 'ssh://deployer@${site}.com:10022/var/git-repos/#{site}.git'

# Default branch is :master
# ask :branch, proc { `git rev-parse --abbrev-ref HEAD`.chomp }

# Default deploy_to directory is /var/www/my_app
set :deploy_to, '/var/www/${site}'

# Default value for :scm is :git
# set :scm, :git

# Default value for :format is :pretty
# set :format, :pretty

# Default value for :log_level is :debug
# set :log_level, :debug

# Default value for :pty is false
# set :pty, true

# Default value for :linked_files is []
# set :linked_files, %w{config/database.yml}

# Default value for linked_dirs is []
set :linked_dirs, %w{bin log tmp/pids tmp/cache tmp/sockets vendor/bundle public/system}

# Default value for default_env is {}
# set :default_env, { path: "/opt/ruby/bin:$PATH" }

# Default value for keep_releases is 5
# set :keep_releases, 5

namespace :deploy do
  %w(start stop restart).each do |command|
    desc '#{command} unicorn server'
    task fetch(:command) do
      on roles(:app), in: :sequence, wait: 5 do
        run "/etc/init.d/unicorn_#{application} #{command}"
      end
    end
  end

  after :restart, :clear_cache do
    on roles(:web), in: :groups, limit: 3, wait: 10 do
      # Here we can do anything such as:
      # within release_path do
      #   execute :rake, 'cache:clear'
      # end
    end
  end
end</pre>

