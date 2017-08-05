---
title: Wheneverを使うRailsプロジェクトをWindowsで触るときの注意点
author: 鉄
type: post
date: 2014-03-28T07:29:47+00:00
url: /2014/rails-project-with-whenever-in-windows/
categories:
  - Rails
  - ruby
  - Windows
  - Windows7

---
`/usr/bin/env: ruby.exe: そのようなファイルやディレクトリはありません`

というエラーが`whenever`で作ったcronのログとして出てきて困ってた。

`bin/rails`の実行権限とか`/usr/bin/env ruby --version` でちゃんとrubyが動いてるかどうか確認したりとか色々。

### 答え

Windowsで作ったRailsプロジェクトだったので `ruby<strong>.exe</strong>`になってた。なんてことだ…。

### 解決策

`bin/rails`の一行目`usr/bin/env ruby.exe`の`.exe`を削除しておきましょう。ふぁっく。

