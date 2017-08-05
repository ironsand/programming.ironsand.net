---
title: rubyで全角半角を考慮して文字の幅を取得
author: 鉄
type: post
date: 2014-04-03T14:54:36+00:00
url: /2014/get-string-size-considering-double-width-and-normal-width-ruby/
categories:
  - ruby

---
文字幅をしるために`全角=2`,`半角=1`で文字サイズが取得したかったので

### やり方

<pre class="lang:ruby decode:true " >"日本語とEnglish".each_char.map{|c| c.ascii_only? ? 1 : 2}.inject(:+)</pre>

Rubyばんざーーい！

### 参考

[2013/02/20/Rubyで全半角混在文字の文字幅を計算する方法 &#8211; ヽ（´・肉・｀）ノログ][1]

