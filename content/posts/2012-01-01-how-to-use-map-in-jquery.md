---
title: jQueryの便利なmapの使い方
author: 鉄
type: post
date: 2012-01-01T02:00:09+00:00
url: /2012/how-to-use-map-in-jquery/
categories:
  - javascript
  - jQuery

---
lispでmapに初めて触れた時は「何、このめんどくさい関数？」と感じ、正直な話あまり触れたくもなかったのですが慣れてくるとこいつはとても便利な賢いやつです。

さてjavascriptでもmapが使えるか調べてみたらjQueryで提供されてました。

mapを使えば配列全部に関数を適用させて、返り値を配列で受け取れます。for文なんて使わなくてもええんやっ！！

### 使い方の例

定番の累乗を求めるサンプル。

<pre>arr = [1,2,3];
arr = $.map(arr, function(n,i){return n*n;});
for(i=0;i&lt;arr.length;i++){
  alert(arr[i]);
}</pre>

サンプルには良く使われるけど、実際にプログラミングしてて累乗が必要になったことがないですね。まあサンプルなんで実用性よりも分かりやすさが重要だから当然といえば当然の話しですね。

とりあえずこんな感じの動作がmapはできます。

### 要素をまとめて取得

たとえばこんなhtmlがあって

<pre>&lt;div&gt;1&lt;/div&gt;
&lt;div&gt;2&lt;/div&gt;
&lt;div&gt;3&lt;/div&gt;</pre>

配列で[1,2,3]が欲しいとする。

**そんな時もこの map を使えば一発解決さ！**(深夜の外人がやってる通販のノリで)

<pre>arr = $("div").map(function(){
    return $(this).text();
  }).get();</pre>

これでとれる。注意点は最後の get()。これがなくても配列っぽいのが返ってくるんだけども、これはjQuery-wrapped arrayというものらしく別物とのこと。

for文で実行したり arr[0] で要素のアクセスしたりはできるけどもjoinすると上手く行かない。このjoinがうまくできないのにはまってだいぶ時間を食われました。

arr.**constructor** でクラスを調べたら

<pre>function Array() {
    [native code]
}</pre>

となるべき所が

<pre>function (a, b) {
    return new e.fn.init(a, b, h);
}</pre>

になってました。この「get() すればよい」という情報を得るためにどれだけ遠回りしたことか…。

とはいえこれで安心してmapをjavascriptでも使えるようになったのでガシガシ使っていこうと思います。

### 参考

<a href="http://api.jquery.com/map/" target="_blank">http://api.jquery.com/map/</a>

