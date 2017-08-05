---
title: irbで`require “foobar”`するのがめんどくさいので楽にする
author: 鉄
type: post
date: 2014-04-30T15:37:39+00:00
url: /2014/require-library-easily-in-irb/
categories:
  - ruby

---
例えば nokogiri でちゃんとデータの取得ができてるか確認するために
  
`irb`を使うために

`$ irb` してから

`require "nokogiri"`と

自分はいつもしてたんですが、めんどくさい。

### 解決策

`$ irb -r nokogiri`な感じでライブラリが読み込めます。ステキ！

