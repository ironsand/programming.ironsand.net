---
title: %w(foo bar) みたいな感じでsymbolを作る方法
author: 鉄
type: post
date: 2014-03-27T13:57:39+00:00
url: /2014/create-a-array-of-symbol-like-string-w/
categories:
  - ruby

---
rubyは文字列の配列を作るときに`["foo", "bar"]` と書くのがめんどくさいからという理由で `%w(foo bar)` みたいな感じで書けちゃいます。

同じような感じで`symbol`もかけないかと思って探してたら`ruby 2.0.0`から`%i`が使えるようになったので
  
`%i(foo bar)` で [:foo, :bar] が書けちゃいます。ステキ！

### 参考

[ruby &#8211; Is there way to create a symbol&apos;s array like string with %w? &#8211; Stack Overflow][1]

