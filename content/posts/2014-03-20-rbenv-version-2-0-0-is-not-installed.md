---
title: 'rbenv: version `2.0.0′ is not installed の対処法'
author: 鉄
type: post
date: 2014-03-20T05:15:06+00:00
url: /2014/rbenv-version-2-0-0-is-not-installed/
categories:
  - Rails
  - ruby
tags:
  - rbenv

---
&#8220;Everyday Rails Testing with RSpec&#8221;を購入して読んでると

サンプルプロジェクトが紹介されてたので`git clone`でダウンロードしてきて `bundle install` をすると

`rbenv: version '2.0.0' is not installed`

と出ちゃって困る。しかも `ruby -v` と確認しようと思ったら再び

`rbenv: version '2.0.0' is not installed`

？？？？？？

「まさか rbenv が壊れた！？」と思って調べてたら、どうやらカレントディレクトリに`.ruby-version`があるとそのバージョンのRubyを参照しようとするために起きるらしい。

### 対策

自分の場合は`2.0.0.p247`が入っているので該当のディレクトリで`rbenv local`すると`.ruby-version`の中身が書き換えられて上手く動くようになりました。

Version自体が異なる場合は上手く動かないと困るので該当のバージョンの ruby を`rbenv install 2.x.x`でインストールしましょう。

