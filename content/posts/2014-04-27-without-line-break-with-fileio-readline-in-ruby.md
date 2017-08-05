---
title: rubyの`FileIO.readline`に改行を含ませないようにする
author: 鉄
type: post
date: 2014-04-26T18:17:15+00:00
url: /2014/without-line-break-with-fileio-readline-in-ruby/
categories:
  - ruby

---
こんなふうにファイルを読み込むと標準では改行が入ってしまいます。

<pre class="lang:ruby decode:true " >File.open(filename,"r") do |f|
  f.readlines
end</pre>

### 解決策

改行はいらないので消しちゃいましょう。

<pre class="lang:ruby decode:true " >File.open(filename,"r") do 
  |f| f.readlines.map &:chomp
end</pre>

