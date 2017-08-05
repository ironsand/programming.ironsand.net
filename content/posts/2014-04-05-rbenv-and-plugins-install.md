---
title: rbenvのインストール方法と入れとくと便利なプラグイン
author: 鉄
type: post
date: 2014-04-04T16:11:27+00:00
url: /2014/rbenv-and-plugins-install/
categories:
  - ruby

---
gitは便利なんだけど、リポジトリ名が長くて暗記できなのがツラい所ですよね。
  
忘れて毎回プラグインのリンクを探すのがめんどくさいのでいつも入れるものをメモっておきます。

### rbenv インストール必須なのまとめ

<pre class="lang:sh decode:true " ># rbenv 本体
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' &gt;&gt; ~/.bash_profile
echo 'eval "$(rbenv init -)"' &gt;&gt; ~/.bash_profile

# Plugins
mkdir ~/.rbenv/plugins
# ほぼ必須。ruby本体入れるのに使う。これ無しで使う方法知らない。
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
# `rbenv rehash`が自動的に
git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash
# `rbenv update`コマンドが使えるように
git clone https://github.com/rkh/rbenv-update.git ~/.rbenv/plugins/rbenv-update
# `rbenv sudo`でsudoでもrbenvが使えるように
git clone git://github.com/dcarley/rbenv-sudo.git ~/.rbenv/plugins/rbenv-sudo
# `rbenv install` するごとに特定のgemをいれる
git clone https://github.com/sstephenson/rbenv-default-gems.git ~/.rbenv/plugins/rbenv-default-gems
</pre>

