---
title: datatimeとtimestampの違いとRailsで知っておくべきこと
author: 鉄
type: post
date: 2014-03-17T19:56:14+00:00
url: /2014/difference-between-datatime-and-timestamp-in-rails/
categories:
  - MySQL
  - Rails
  - ruby

---
何回か調べたけど未だに覚えられてないのでもう一度調べ直しました。

確か前回調べたときは英語読むのがめんどくさいから日本語の情報を見て納得したんですが、今回はめんどくさがらずに英語圏で検索したらいつも通りStackOverflowにて大変わかりやすい答えが見つかりました。ありがたや〜。 (人´∀｀)

### datatime と timestamp の違い

`datatime` が 1000年から9999年までを表現して `timestamp` は `unix timestamp`のフロントエンドに過ぎないので 1970年から2038年までしか扱えない。

扱う範囲が違うので`datatime`が8バイト`timestamp`が4バイト使う。

### Rails における扱い。

これが一番重要な気がするけど、Railsでは**どちらを指定してもデータベースには`DATATIME`型で保存される**。

何故かこのことについて述べてるサイトがあんまりなかったのでこの記事を書いておきました。

### 参考

[In Ruby on Rails, what&apos;s the difference between DateTime, Timestamp, Time and Date? &#8211; Stack Overflow][1]

