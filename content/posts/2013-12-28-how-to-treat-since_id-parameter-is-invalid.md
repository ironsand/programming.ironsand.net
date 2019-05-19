---
title: '"since_id parameter is invalid."と言われた時の対処法'
author: 鉄
type: post
date: 2013-12-27T19:14:15+00:00
url: /2013/how-to-treat-since_id-parameter-is-invalid/
categories:
  - Rails
  - ruby
---
Railscasts のTwitter の項目通りに書いてると `since_id parameter is invalid.` のエラーでつまづきました。

どうやらTwitterAPI1.1からの変更で `since_id` に `` を指定できなくなったのが原因のようです。

もちろんレコードにすでにつぶやきが入ってれば問題ないんですが初回の何も入ってない時にこけてしまうわけです。

### 対策

<pre class="lang:ruby decode:true " >user.twitter.list_timeline(list_id, since_id: [maximum(:tweet_id),"1"].max)</pre>

と返り値に最低でも`1`が入るようにしておけばOKです。文字列にしてるのは `twitter_id`を文字列で保持してるからです。

### 参考

[API v1.1 statuses/user\_timeline since\_id parameter is invalid | Twitter Developers][1]

