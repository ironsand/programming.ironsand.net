---
title: rubyで文字列を正規表現で分類してグループ分けする
author: 鉄
type: post
date: 2014-03-17T15:58:02+00:00
url: /2014/group-strings-by-similar-pattern-with-ruby/
categories:
  - ruby

---
最後の数字だけ違う文字列をグループ分けしたかったんですが、自分で書いてみるとこんな面倒くさい感じになって (´・ω・｀)ｼｮﾎﾞｰﾝ

<pre class="lang:ruby decode:true " >a1 = %w(foo1 foo2 foo3 bar1 bar3 buz2)
a2 = a1.map{|v| v.sub(/[0-9]$/,"")}.uniq

tmp = Array.new(a2.size)
a2.each_with_index do |v2, i|
  a1.each do |v1|
    if v1.sub(/[0-9]$/, "") == v2
      tmp[i].nil? ? tmp[i] = [v1] : tmp[i].push(v1)
    end
  end
end

p tmp # =&gt; [["foo1", "foo2", "foo3"], ["bar1", "bar3"], ["buz2"]]</pre>

なので、調べてみたら非常に簡単な方法が見つかりました。

<pre class="lang:ruby decode:true " >a1 = %w(foo1 foo2 foo3 bar1 bar3 buz2)
p a1.group_by{|x| x[/[a-zA-Z]+/] }.values</pre>

Rubyすげぇ！

### 参考

[arrays &#8211; Group strings with similar pattern in Ruby &#8211; Stack Overflow][1]

