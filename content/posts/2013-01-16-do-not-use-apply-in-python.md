---
title: Pythonのapplyを使う時の注意点、…というか使っちゃダメ。
author: 鉄
type: post
date: 2013-01-15T18:02:10+00:00
url: /2013/do-not-use-apply-in-python/
categories:
  - python

---
Lispを書いてると、他の言語でもapplyを使いたくなる。

そしてPythonにもapplyがあったので早速喜んで使ってたら引数の数がおかしいというエラーメッセージに困らされた。

### 基本的なapplyの使い方

`</p>
<pre>def hoge(word):
    print word

apply(hoge,"A")</pre>
<p>`

とまあこんな感じ使うわけです。

### 文字列を引数にできない。

ところがこの**引数の&#8221;A&#8221;を&#8221;ABC&#8221;に変えるだけでエラー**になる。
  
`</p>
<pre>Traceback (most recent call last):
  File "<stdin>", line 9, in <module>
TypeError: hoge() takes exactly 1 argument (3 given)</pre>
<p>`

どうやら文字列を渡すと文字数分だけの引数を渡したと解釈されてしまうらしい。

### 解決策

さて、解決方法ですがタイトルにもあるように廃止された関数なのでもう使っちゃダメらしい。

> 引数 function は呼び出しができるオブジェクト (ユーザ定義 および組み込みの関数またはメソッド、またはクラスオブジェクト) でなければなりません。args はシーケンス型でなくてはなりません。 function は引数リスト args を使って呼び出されます; 引数の数はタプルの長さになります。オプションの引数 keywords を与える場合、 keywords は文字列のキーを持つ辞書で なければなりません。これは引数リストの最後に追加されるキーワード 引数です。 apply() の呼び出しは、単なる function(args) の呼び出しとは異なります。 というのは、apply() の場合、引数は常に一つだから です。**apply() は function(\*args, \**keywords) を 使うのと等価です。** 上のような &#8220;拡張された関数呼び出し構文&#8221; は apply() と全く等価なので、必ずしも apply() を使う必要はありません。
  
> リリース 2.3 で撤廃されました。 上で述べられたような拡張呼び出し構文を使って ください。

自分にはよくわからないですが<p style=color:red;>applyでやりたいことは function(\*args, \**keywords) で全部できるから applyは使うな。</p> 

ということのようです。

&#8220;Python Apply&#8221;をキーワードにしてGoogle検索しても「使ってはいけない」という情報がぱっと出て来なかったのでこの記事を書きました。よくわからないエラーで困ってる誰かの参考になれば幸いです。

### 参考

2.2 非必須組み込み関数 (Non-essential Built-in Functions)  
<http://docs.python.jp/2.5/lib/non-essential-built-in-funcs.html>

