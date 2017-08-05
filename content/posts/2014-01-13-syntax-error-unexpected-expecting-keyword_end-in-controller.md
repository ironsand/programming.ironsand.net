---
title: Controllerで出る`syntax error, unexpected ‘:’, expecting keyword_end`エラー
author: 鉄
type: post
date: 2014-01-13T09:44:32+00:00
url: /2014/syntax-error-unexpected-expecting-keyword_end-in-controller/
categories:
  - Rails
  - ruby

---
<pre class="lang:default decode:true " >yntax error, unexpected ':', expecting keyword_end</pre>

といつもの見慣れたようなTypoのエラーが出たのでControllerを確認したけどない。何度見てもちゃんとカッコ閉じてるし `end` も使ってる。なのにエラーが消えない！

### 解決

モデルのほうで `has_many: words` って書いてました。 正しくは `has_many :words` ですね。悲しい。こんなものに結構な時間を着いたしたのが悲しい。

