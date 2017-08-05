---
title: Gemfileを開いてたらsmart-compileで`bundle install`を実行する
author: 鉄
type: post
date: 2013-12-15T07:33:43+00:00
url: /2013/run-bundle-install-to-gemfile-with-smart-compile-in-emacs/
categories:
  - Editor
  - Emacs
  - Rails
  - ruby

---
開いてるファイルをそのまま実行できる`smart-compile`でGemfileを開いてたら`bundle install`を実行したかったのでやり方を調べてみました。

### 設定方法

どうやらsmart compile は自動的にコマンドの実行ディレクトリをファイルがある場所に移動してくれるようなので単純に `Gemfile`というファイル名と`bundle install`のコマンドを他のファイルと同じように紐付ければOKのようです。

<pre class="lang:lisp decode:true " title="~/.emacs.c/inits/30-smart-compile.el" >(global-set-key (kbd "C-c C-x") 'smart-compile)
  (setq smart-compile-alist
      (append
       '(("\\.rb$" . "ruby %f"))
       '(("\\.php$" . "php %f"))
       '(("\Gemfile$" . "bundle install"))
       smart-compile-alist))</pre>

もちろん ruby や php を使ってなかったら該当行は必要ありません。

### 使い方

これで Gemfile を開いて `C-c C-x` するとこんな風に `bundle install` が実行されます。

<pre class="lang:ps decode:true " >-*- mode: compilation; default-directory: "~/dev/foo/" -*-
Compilation started at Sun Dec 15 16:29:42

bundle install
Using rake (10.1.0) 
Using i18n (0.6.9) from git://github.com/svenfuchs/i18n.git (at master) 
Using minitest (4.7.5) 
Using multi_json (1.8.2) 
Using atomic (1.1.14) 
Using thread_safe (0.1.3) 
Using tzinfo (0.3.38) 
Using activesupport (4.0.0) 
Using builder (3.1.4) 
Using erubis (2.7.0) 
Using rack (1.5.2) 
Using rack-test (0.6.2) 
Using actionpack (4.0.0) 
Using mime-types (1.25.1) 
Using polyglot (0.3.3) 
Using treetop (1.4.15) 
Using mail (2.5.4) 
Using actionmailer (4.0.0) 
Using activemodel (4.0.0) 
Using activerecord-deprecated_finders (1.0.3) 
Using arel (4.0.1) 
Using activerecord (4.0.0) 
Using sass (3.2.12) 
Using bootstrap-sass (3.0.3.0) 
Using will_paginate (3.0.5) 
Using bootstrap-will_paginate (0.0.10) 
Using mini_portile (0.5.2) 
Using nokogiri (1.6.0) 
Using xpath (2.0.0) 
Using capybara (2.2.0) 
Using timers (1.1.0) 
Using celluloid (0.15.2) 
Using ffi (1.9.3) 
Using childprocess (0.3.9) 
Using coderay (1.1.0) 
Using coffee-script-source (1.6.3) 
Using execjs (2.0.2) 
Using coffee-script (2.2.0) 
Using thor (0.18.1) 
Using railties (4.0.0) 
Using coffee-rails (4.0.1) 
Using diff-lcs (1.2.5) 
Using factory_girl (4.3.0) 
Using factory_girl_rails (4.3.0) 
Using faker (1.2.0) 
Using formatador (0.2.4) 
Using friendly_id (5.0.2) 
Using rb-fsevent (0.9.3) 
Using rb-inotify (0.9.2) 
Using listen (2.4.0) 
Using lumberjack (1.0.4) 
Using method_source (0.8.2) 
Using slop (3.4.7) 
Using pry (0.9.12.4) 
Using guard (2.2.4) 
Using rspec-core (2.14.7) 
Using rspec-expectations (2.14.4) 
Using rspec-mocks (2.14.4) 
Using rspec (2.14.1) 
Using guard-rspec (4.2.0) 
Using spork (1.0.0rc4) 
Using guard-spork (1.5.1) 
Using hike (1.2.3) 
Using jbuilder (1.5.3) 
Using jquery-rails (3.0.4) 
Using json (1.8.1) 
Using bundler (1.3.5) 
Using tilt (1.4.1) 
Using sprockets (2.10.1) 
Using sprockets-rails (2.0.1) 
Using rails (4.0.0) 
Using rdoc (3.12.2) 
Using rspec-rails (2.14.0) 
Using sass-rails (4.0.1) 
Using sdoc (0.3.20) 
Using spork-rails (4.0.0) 
Using sqlite3 (1.3.8) 
Using turbolinks (2.0.0) 
Using uglifier (2.3.3) 
[32mYour bundle is complete![0m
[32mIt was installed into ./vendor/bundle[0m

Compilation finished at Sun Dec 15 16:29:45
</pre>

