---
title: Helperメソッド内で form_tag を使うときの注意点
author: 鉄
type: post
date: 2015-02-20T02:30:59+00:00
url: /2015/helperメソッド内で-form_tag-を使うときの注意点/
categories:
  - Rails
  - ruby

---
`form_tag`を使えばブロック内の全体を返してくれるかと思ったのですが、そうではないらしく最終行だけ返ってきてしまいます。

### 具体例

つまり

<pre class="lang:ruby decode:true " >def generate_form(path)
  form_tag(path) do
    input_tag
    submit_tag
  end
end</pre>

だとフォームそのものと最終行の`submit_tag`だけが表示されてその他の入力フィールドが一切表示されません。

### 対策

なので以下のように毎行`String`を保存しておきましょう。何でこんな仕様になってるんだろう…？

<pre class="lang:ruby decode:true " >def generate_form(path)
  form_tag(path) do
    str = input_tag
    str += submit_tag
    str
  end
end</pre>

### 参考

[ruby on rails &#8211; How do I use form_tag from within a helper? &#8211; Stack Overflow][1]

