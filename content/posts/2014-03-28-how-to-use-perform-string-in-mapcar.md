---
title: xyzzyのmapcar 内で perform-string を使うときの注意点
author: 鉄
type: post
date: 2014-03-28T03:34:03+00:00
url: /2014/how-to-use-perform-string-in-mapcar/
categories:
  - Editor
  - xyzzy

---
mapcar で perform-string を使って文字列置換しようと思ってかなりハマったのでメモって置きます。

### ダメな例

<pre class="lang:lisp decode:true " >(mapcar '(lambda (s)
              (goto-char (point-min))
              (perform-replace s "" nil t t nil))
            '("foo[0-9]" "bar[0-9]"))</pre>

これだと &#8220;foo1 bar2&#8221; は削除できるけど &#8220;bar2&#8221; と2個めの検索要素だけしかないときに削除できない

### 良い例

<pre class="lang:lisp decode:true " >(mapcar '(lambda (s)
              (goto-char (point-min))
              (perform-replace s "" nil t t t))
            '("foo[0-9]" "bar[0-9]"))</pre>

`perform-replace`の最後の引数`NOERROR`を`t`に設定しておけば該当する文字列がなくてもスムーズに次に進んでくれます。

