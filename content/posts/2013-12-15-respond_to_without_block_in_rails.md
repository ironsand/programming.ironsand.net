---
title: respond_to を ブロックを使わずに書く。
author: 鉄
type: post
date: 2013-12-15T09:29:01+00:00
url: /2013/respond_to_without_block_in_rails/
categories:
  - Rails
  - ruby

---
Ajaxの処理をRailsでするときはControllerに

<pre class="lang:ruby decode:true " >respond_to do |format|
  format.js
end</pre>

と書いてたんですが、いちいちブロック引数に format を使って処理するのは無駄な気がしたので一行で書ける方法を調べてみた。

### 解決策

<pre class="lang:ruby decode:true " >respond_to :js</pre>

でOKでした。

<pre class="lang:ruby decode:true " >respond_to :html, :js</pre>

な書き方もOKなようです。

### 参考

[respond_to (ActionController::MimeResponds::InstanceMethods) &#8211; APIdock][1]

