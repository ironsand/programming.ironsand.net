---
title: 動的に追加したDOM要素にhoverイベントリスナーを追加する
author: 鉄
type: post
date: 2014-01-31T15:25:08+00:00
url: /2014/add-event-listener-to-dynamically-appended-elements/
categories:
  - coffee
  - javascript
  - jQuery

---
かなりハマったので`append()`などを使って動的に追加したHTMLの要素に`hover`イベントを追加する方法を残しておきます。説明は全部 coffee script で書いてるので生のJSが良い人は自動変換サービスでもをつかってください。

### 前提となる知識

まず基本として `$('#foo').click -> console.log "押された！"` のように `#foo` に対して click イベントが追加されているわけですが、このイベントの追加はページの読み込み時に行われるために `append()` などで後から動的に追加された要素にはイベントの登録がされません。

なのでそれを解決するために昔の `delegate()`, 今なら `on()` メソッドがあるわけです。簡単でわかり易い名前に統一されたので見た目はスッキリしたのですが、代わりにサンプルコードを探すのが大変になりました。 `on` って単語短すぎやしません…？

### 後から追加された要素に click イベントを追加

前置きが長くなりましたが

<pre class="lang:coffee decode:true " >$('#foo').click -&gt; console.log "押された！"</pre>

を動的に追加された要素に適用させるには

<pre class="lang:coffee decode:true " >$(document).on 'click', '#foo', -&gt; console.log "押された！"
</pre>

とします。`document` 内部の要素がクリックされるたびにイベントが発火され、クリック対象が `#foo` ならメソッドが実行されます。もちろん `document` ではなくページ読み込み時に存在する `#foo` の親に当たる要素なら何でも構いません。無駄なイベントを発生させないためにできるだけ近い親が良いでしょう。

### 後から追加された要素に hover イベントを追加

<del datetime="2014-02-01T01:35:53+00:00">同様に <code>hover</code> イベントも click イベントのように簡単に書き換えれたらいいのですが、hover イベントを <code>on()</code> を使って割り当てると <code>hover</code> は <code>mouseenter</code> と <code>mouseleave</code>という複数のイベントを受け取っており、このように複数のイベントを受け取ってる関数を <code>on</code> メソッドで割り当てるためにはどのイベントを受け取ったのかを判別して処理する必要が出てきます。</del>

記述が間違っていたので修正しました。
  
`on`イベントの引数として `"hover"`を使った場合、それは単なる `"mouseenter mouseleave"` の別名であって `hover()` 関数とは無関係であり、またこの記述方法は jQuery1.8 で depracated で 1.9 では削除されたそうです。

以下はマウスカーソルがあたった時に、クリックできる要素だとユーザーに伝えるためにマウスの形状を変更するコードですが

<pre class="lang:coffee decode:true " >$('#foo').hover \
  (-&gt; $(@).css "cursor", "pointer"), \
  (-&gt; $(@).css "cursor", "default")</pre>

のようなコードがあった時に

<pre class="lang:coffee decode:true " >$(document).on 'hover', '#foo', \
  (-&gt; $(@).css "cursor", "pointer"), \
  (-&gt; $(@).css "cursor", "default")</pre>

では**動きません。**

### 解決策

実際に動くコードは以下のようになります。

<pre class="lang:coffee decode:true " >$(document).on
    mouseenter: -&gt; $(@).css "cursor", "pointer",
    mouseleave: -&gt; $(@).css "cursor", "default"
  , '#foo'</pre>

### 参考

[javascript &#8211; JQuery .on() method with multiple event handlers to one selector &#8211; Stack Overflow][1]

[.on() | jQuery API Documentation][2]

