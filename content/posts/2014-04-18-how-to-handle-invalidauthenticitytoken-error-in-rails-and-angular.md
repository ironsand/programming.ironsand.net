---
title: Rails+Angular.js で InvalidAuthenticityTokenエラーが出るときの対処法
author: 鉄
type: post
date: 2014-04-17T18:37:04+00:00
url: /2014/how-to-handle-invalidauthenticitytoken-error-in-rails-and-angular/
categories:
  - AngularJS
  - Rails
  - ruby

---
RailsのDBからGETでデータの呼び出しはできるけど、PUTで値の追加ができなくてこんなエラーに成った時の対処法

<pre class="lang:default decode:true " >Completed 422 Unprocessable Entity in 126ms

ActionController::InvalidAuthenticityToken - ActionController::InvalidAuthenticityToken:</pre>

### 原因

CSRF対策です。

### ダメな対策

モデルにこれを追加

<pre class="lang:ruby decode:true " >skip_before_filter :verify_authenticity_token</pre>

サイバーノーガード戦法です。おすすめしません。

### 良さそうな対策

gem の`<a href="https://github.com/xrd/ng-rails-csrf">ns-csrf-rails</a>`を使う。わからないことは全部gemにまかせてしまいましょう。

