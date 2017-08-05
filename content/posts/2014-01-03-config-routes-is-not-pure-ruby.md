---
title: `config/routes.rb`内のブロックはブロックじゃない。
author: 鉄
type: post
date: 2014-01-03T06:19:02+00:00
url: /2014/config-routes-is-not-pure-ruby/
categories:
  - Rails
  - ruby

---
<pre class="lang:ruby decode:true " >scope "api" do
    resources :entries
  end</pre>

このコードをワンラインで、

<pre class="lang:ruby decode:true " >scope "api" { resources :entries }</pre>

とかくと動かないので、routes.rb は DSLなのでブロックの書き方に影響が出てるようです。何でこうしてるかの詳しい理由はよくわからない。

