---
title: Macで`gem install rmagick`がコケる時の対処法
author: 鉄
type: post
date: 2014-01-27T09:24:19+00:00
url: /2014/gem-install-rmagic-in-maverick/
categories:
  - Mac
  - Rails
  - ruby

---
画像編集をRailsでしたかったので `ImageMagick` を Railsから使うgem `rmagick` をインストールしようと思ったらこんなエラーが出てしまった。環境は Maverick。

<pre class="lang:default decode:true " >Can't install RMagick 2.13.1. Can't find the ImageMagick library or one of the dependent libraries. Check the mkmf.log file for more detailed information.

*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.</pre>

### 解決策

最新版の `2.13.2` をインストールすればOK。ちなみにライブラリのリンクを作るという方法も紹介されてましたがこっちは失敗。

`gem install rmagick -v '2.13.2'` でインストールしましょう。

ドキュメントのインストールの時に `unable to convert "¥xCF" from ASCII-8BIT to UTF-8 for なんたらこうたら`というエラーが大量に出ましたがインストール自体は正常に動いてるようです。

### 参考

[imagemagick &#8211; Error installing Rmagick on Mountain Lion &#8211; Stack Overflow][1]

