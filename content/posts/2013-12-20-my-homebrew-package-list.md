---
title: homebrewでインストールパッケージリスト俺用
author: 鉄
type: post
date: 2013-12-20T02:24:34+00:00
url: /2013/my-homebrew-package-list/
categories:
  - Mac

---
さっきの記事でも書きましたが、Macを入れなおしてます。
  
今度は homebrew で入れるパッケージのリストです。

<pre class="lang:sh decode:true " >brew install --HEAD ruby-build
brew tap josegonzalez/php
# --universalオプションが無いとwineがこける
brew install jpeg libpng --universal 
# php用
brew install freetype gd
brew link libpng freetype jpeg
brew install php55
brew install rbenv openssl readline mysql  postgresql wget wine graphviz imagemagick nginx node 
brew install macvim --override-system-vim
# Applicationsフォルダに置く
brew linkapps
</pre>

アホみたいにエラーが出るので `brew doctor`で出てくるのに全部対処しましょう。

