---
title: WindowsのRailsでtwitter-bootstrap-railsを使う方法
author: 鉄
type: post
date: 2014-04-20T09:13:20+00:00
url: /2014/how-to-use-twitter-bootstrap-rails-in-windows/
categories:
  - CSS
  - Rails
  - ruby
  - Sass
  - Windows

---
`twitter-bootstrap-rails`を普通にWindowsで使おうとすると`libv8がないからアカンで～`的なエラーが出てきてインストールに失敗します。

### 対策

特定のバージョンはインストールできるのでそれをインストールしましょう。

`gem install libv8 --version 3.11.8.0`

あとは`Gemfile`に`gem 'therubyracer', platforms: :ruby`のコメントアウトを外して`gem twitter-bottstrap-rails`を追加すれば万事OK！

### 追記、より良い解決策

そもそも`bootstrap-sass`を使えばよいのでは？

