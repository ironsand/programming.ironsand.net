---
title: Maverickで`rails new` が `atomic`のインストールでこける時の対処法
author: 鉄
type: post
date: 2014-01-03T04:07:31+00:00
url: /2014/fail-to-bundle-install-in-maverick/
categories:
  - Rails
  - ruby
tags:
  - Maverick

---
`rails new` したらbundle install が `atomic` の所でコケた。何か前も同じエラーに引っかかって結構検索した記憶があったんだけど今回も対処法を探すのに結構な時間がかかってしまった。

エラーメッセージはこんなの。

<pre class="lang:sh decode:true " >run  bundle install
Fetching gem metadata from https://rubygems.org/..........
Fetching gem metadata from https://rubygems.org/..
Resolving dependencies.........
Installing rake (10.1.1) 
Installing i18n (0.6.9) 
Installing minitest (4.7.5) 
Installing multi_json (1.8.2) 
Installing atomic (1.1.14) 
Gem::Installer::ExtensionBuildError: ERROR: Failed to build gem native extension.

    /Users/ironsand/.rbenv/versions/2.0.0-p247/bin/ruby extconf.rb 
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
    --with-opt-dir
    --without-opt-dir
    --with-opt-include
    --without-opt-include=${opt-dir}/include
    --with-opt-lib
    --without-opt-lib=${opt-dir}/lib
    --with-make-prog
    --without-make-prog
    --srcdir=.
    --curdir
    --ruby=/Users/ironsand/.rbenv/versions/2.0.0-p247/bin/ruby
    --with-atomic_reference-dir
    --without-atomic_reference-dir
    --with-atomic_reference-include
    --without-atomic_reference-include=${atomic_reference-dir}/include
    --with-atomic_reference-lib
    --without-atomic_reference-lib=${atomic_reference-dir}/
/Users/ironsand/.rbenv/versions/2.0.0-p247/lib/ruby/2.0.0/mkmf.rb:430:in `try_do': The compiler failed to generate an executable file. (RuntimeError)
You have to install development tools first.
    from /Users/ironsand/.rbenv/versions/2.0.0-p247/lib/ruby/2.0.0/mkmf.rb:515:in `try_link0'
    from /Users/ironsand/.rbenv/versions/2.0.0-p247/lib/ruby/2.0.0/mkmf.rb:813:in `try_run'
    from extconf.rb:26:in `&lt;main&gt;'


Gem files will remain installed in /Users/ironsand/dev/raffler/vendor/bundle/gems/atomic-1.1.14 for inspection.
Results logged to /Users/ironsand/dev/raffler/vendor/bundle/gems/atomic-1.1.14/ext/gem_make.out
An error occurred while installing atomic (1.1.14), and Bundler cannot continue.
Make sure that `gem install atomic -v '1.1.14'` succeeds before bundling.
ironsand@Air-2 dev$ gem update
</pre>

### 解決策

エラーメッセージからだと全くわからないんだけれども、どうやらこれは Xcodeのバージョンをアップとか新規インストールした時に一度立ち上げて利用規約にOKと答えておかないとコンパイラーが使えずにでるらしい。

なので、Xcodeを一度立ち上げて規約にOKしたら解決。と前回はここで解決したんですがどうやら今回はこれだけじゃだめらしい。

### 今度こそ解決策

Commandline toolsを再インストールするために `xcode-select --install`したら解決しました！
  
Maverickに上げたのが原因らしいです。
  
自分の場合はターミナルの再起動するまでCommandline toolsのアップデートが認識できませんでしたが必須なのかどうかはわかりません。

### 参考

[Ruby &#8211; Mac OS X 10.9 Mavericks で Rails の `bundle install` に失敗する件の対処法 &#8211; Qiita [キータ]][1]

