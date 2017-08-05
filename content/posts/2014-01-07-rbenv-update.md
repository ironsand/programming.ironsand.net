---
title: rbenv を最新の状態にupdate する
author: 鉄
type: post
date: 2014-01-07T13:46:26+00:00
url: /2014/rbenv-update/
categories:
  - ruby
  - さくらのVPS

---
ruby 2.1.0 も出たことだし、とりあえずさくらVPSにおいてるCentOS上に入れておこうと思ったけど、ちょっと古いバージョンしか `rbenv install --list` で出てくれない。

`rbenv update`という便利なコマンドはないようなのでアップデート方法を調べてアップデートしてみた。

### アップデート方法

どうやってインストールしたかは全く覚えてなかったけど調べてみるとどうやら `git clone` でインストールしたっぽいので `cd ~/.rbenv; git pull` するだけでOKらしい。

無事にアップデートできたのでもう一度インストールできるrubyのバージョンを確認したら ない。ない。

どうやらrubyのインストールには `ruby-build`を使ってるのでそっちをアップデートしないとインストール可能なバージョンは更新されないらしい。ちなみに存在しないバージョンのインストールを試みるとこんな感じに教えてくれる。

<pre class="lang:sh decode:true " >ironsand@SarakuVPS ~$ rbenv install 2.0.0-p247
ruby-build: definition not found: 2.0.0-p247

You can list all available versions with `rbenv install --list'.

If the version you're looking for is not present, first try upgrading
ruby-build. If it's still missing, open a request on the ruby-build
issue tracker: https://github.com/sstephenson/ruby-build/issues</pre>

### ruby-build のアップデート

ruby-buildも`git clone`してるだけなので、 `cd .rbenv/plugins/ruby-build/; git pull` すれば最新の状態に反映される。後はいつも通り `rbenv install --list` して `2.1.0` があることを確認して `rbenv install 2.1.0` でインストールできる。時間がかかるので放置しときましょう。

