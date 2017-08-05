---
title: Railsで ‘not null’ の制限をマイグレーションで取り除く方法
author: 鉄
type: post
date: 2013-12-23T05:25:01+00:00
url: /2013/remove-constraints-from-a-user-model-in-rails/
categories:
  - Rails
  - ruby

---
devise と omniauthを組みわせて使うと default の `email` と `encrypted_password` が必ず値を持たなければならない `null => false` の制限が邪魔だったのでMigrationで削除しようとしたけど方法がわからなかったので調べてみた。

### やりかた

<pre class="lang:ruby decode:true " >class RemoveConditionFromUser &lt; ActiveRecord::Migration
  def change
    change_column :users, :email, :string, null: true
    change_column :users, :encrypted_password, :string, null: true    
  end
end</pre>

### 参考

[Rails Migration: Remove constraint &#8211; Stack Overflow][1]

