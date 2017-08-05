---
title: File.write みたいに File.append も使いたい
author: 鉄
type: post
date: 2016-03-28T01:35:03+00:00
url: /2016/file-write-みたいに-file-append-も使いたい/
nkweb_code_in_head:
  - default
nkweb_Use_Custom_js:
  - default
nkweb_Use_Custom_Values:
  - default
nkweb_Use_Custom:
  - 'false'
categories:
  - ruby

---
`File.write(filename, text)`でファイルに書き込みできるの便利ですよね。

でも、`File.append`は用意されてないので`File.open(filename, 'a'){|f| f.write(text)}`のように書かなきゃいけません。めんどくさい。

なのでめんどくさくないように定義しましょう。やっぱり既存クラスのメソッド拡張ができるRubyはいいですね。

<pre class="lang:ruby decode:true " title="file_append.rb" >class File
  def self.append(filename, text)
    File.open(filename, 'a'){|f| f.write(text)}
  end
end</pre>

