---
title: Capyparaで `undefined method `visit’`と出る時の対処法
author: 鉄
type: post
date: 2014-01-09T08:55:19+00:00
url: /2014/how-to-solve-capypara-undefined-method-visit/
categories:
  - Rails
  - ruby

---
「Rspecよくわかんねー。」という思いを胸に抱き続けてきましたが、やっぱりやらないとダメっぽいので使おうとしたら早速 `undefined method 'visit'`と言われて困る。

### 原因

このエラーの原因はCapybaraが最近のアップデートでこっそりと対象のディレクトリを `requests` から `features` に変えたのが原因らしいです。やめてほしいそういうの。

しかも [Google group][1] にこっそり報告してるだけ。もっと こえを おおきく。

### 解決策

`spec_helper.rb` に以下をたす解決策もあるそうですが、将来的に requests じゃなくてfeatures を使うという意向ならそうしたほうが楽そうなので `mv spec/requests/ spec/features` して自分は対策しました。

ちなみに `spec_helper.rb`に足す場合はこちら。

<pre class="lang:default decode:true " title="spec/spec_helper.rb" >require 'capybara/rails'
require 'capybara/rspec'
include Capybara::DSL</pre>

### 参考

[ruby on rails &#8211; Capybara: undefined method &apos;visit&apos; &#8211; Stack Overflow][2]

[rails 3.2でRspecを導入したけど NameError &#8211; undefined method \`visit&apos; って出るときの対策 &#8211; どぶんけーブログ][3]

