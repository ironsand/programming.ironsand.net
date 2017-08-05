---
title: rails の `blank?` メソッドを jQuery に追加する方法
author: 鉄
type: post
date: 2013-12-29T00:34:06+00:00
url: /2013/jquery-isblank-function/
categories:
  - coffee
  - javascript
  - jQuery

---
rails には 値の有無をチェックするときにタブやスペースなどの空白が入っていても「空」だと判断する便利な `blank?` 関数が用意されていますが、どうやら JavaScript や jQuery には用意されてないので追加してみました。

自分で書いた後にもっと良さそうなコードを見つけたのでそちらを紹介します。

### JavaScript

<pre class="lang:js decode:true " title="isBlank.js" >$.fn.isBlank = function() {
  return !$(this.html()) || $.trim($(this).html()) === "";
};
</pre>

### Coffee

もちろん Rails 標準のCoffeeも。

<pre class="lang:coffee decode:true " >$.fn.isBlank = ->
  !$(@.html()) || $.trim($(@).html()) is ""</pre>

### 参考

[Checking for blank input with jQuery &#8211; Stack Overflow][1]

[jQuery isBlank() | LakTEK (Lakshan Perera)][2]

