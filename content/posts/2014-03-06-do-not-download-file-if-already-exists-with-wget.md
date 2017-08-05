---
title: wget でファイルが既に存在したらダウンロードしない方法
author: 鉄
type: post
date: 2014-03-06T08:55:52+00:00
url: /2014/do-not-download-file-if-already-exists-with-wget/
categories:
  - Commands
  - wget

---
`wget`で同じファイル、例えば`foo.zip`をもう一度ダウンロードすると `foo.zip.1`と自動的に別名でファイルを保存してくれるんですが、自動処理の中で使う時に毎回ダウンロードしたくない時にはちょっとめんどくさい。

### 既に存在する時はダウンロードをスキップ方法

`wget`には`--no-clobber`もしくはそれの省略形 `-nc` という上書きを禁止するオプションがあるのでそれを使いましょう。

ちなみに &#8220;clobber&#8221; は「不注意に上書きをしてファイルを破壊してしまう。」という意味の英単語です。

### 参考

[wget &#8211; skip if files exist? &#8211; Stack Overflow][1]

