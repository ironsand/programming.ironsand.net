---
title: Deviseのユーザーを`rake db:seed`で追加する
author: 鉄
type: post
date: 2014-03-30T21:08:01+00:00
url: /2014/how-to-add-devise-user-by-rake-db-seed/
categories:
  - Rails
  - ruby

---
`db/seeds.rb`に`User.create`で`encrypted_password`を与えてDeviseのユーザーを作ろうとしたら失敗した。

### 原因

passwordが存在しないために`validation`に引っかかってしまってる。

### 対策

`password`を平文で打てば解決するらしいけど、平文のパスワードは使いたくないのでバリデーションの方を無効化してしまいましょう。

`User.new(email: someone@example.com).save(validate: false)`

でOKです。`encrypted_password`の取得方法は色々あるでしょうが、自分の場合は一度Deviseで作ってからそれを`rails console`使って`User.first.encrypted_password`を取ってきました。

### 参考

[Cannot create Devise account using rake db:seed for Rails 3.0 &#8211; Stack Overflow][1]

