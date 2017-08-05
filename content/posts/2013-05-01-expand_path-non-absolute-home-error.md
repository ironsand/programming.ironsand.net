---
title: 'Railsで新規プロジェクトを作ろうとすると`expand_path’: non-absolute homeというエラーが出る'
author: 鉄
type: post
date: 2013-05-01T03:12:23+00:00
url: /2013/expand_path-non-absolute-home-error/
categories:
  - Rails
  - ruby

---
`rails new hoge`

とすると

`` `expand_path': non-absolute home ``

というエラーが出てしまって「Windowsだしなあ。」と諦めかけてたけど、このhomeというのは環境変数のHOMEのことらしく、確かにcygwinを使う時のためにHOMEに /cygdrive/ から始まる値を入れてたのを思い出したので環境変数 HOME を削除してみたら動いた。

ちなみに irb もHOMEに入ってる値によっては動かないらしい。

### 参考

\`expand_path&apos;: non-absolute home  
<http://devnet.jetbrains.com/thread/437313>

