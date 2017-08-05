---
title: jQueryで要素の存在を確認する `isExist()` と `isNotExist()` を定義する
author: 鉄
type: post
date: 2013-12-30T02:45:45+00:00
url: /2013/check-existance-of-element-with-jquery/
categories:
  - coffee
  - javascript
  - jQuery

---
jQuery で選択した要素が存在するかどうかの関数が何故か用意されてないようだったので追加しました。

CoffeeScriptで書いてるのでjavascriptとして使いたい場合は converter にかけてください。

<pre class="lang:coffee decode:true " >$.fn.isExist = -&gt;
  $(@).length != 0
$.fn.isNotExist = -&gt;
  $(@).length == 0   </pre>

### 参考

[How to tell if an element exists | jQuery for Designers &#8211; Tutorials and screencasts][1]

