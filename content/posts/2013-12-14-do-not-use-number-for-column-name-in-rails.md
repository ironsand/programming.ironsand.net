---
title: Railsのカラム名の語頭に数字を使ってはいけない
author: 鉄
type: post
date: 2013-12-14T08:08:39+00:00
url: /2013/do-not-use-number-for-column-name-in-rails/
categories:
  - Rails
  - ruby

---
Railsの学習がてらに2chもどきをつくろうと思って \`rails new 2ch\` してみるとエラーになる。これはいいんだけど、\`rails generate Model 2ch\` ってエラーを吐かないのに実際は使えないので修正がめんどくさくなるので気をつけましょう。

