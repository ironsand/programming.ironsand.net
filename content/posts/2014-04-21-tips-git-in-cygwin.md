---
title: cygwinのgitを使うときの注意点
author: 鉄
type: post
date: 2014-04-20T23:02:04+00:00
url: /2014/tips-git-in-cygwin/
categories:
  - Commands
  - cygwin
  - git

---
cygwinはWindows上で作成されたファイルを全て`755`の実行可能ファイルとして扱ってしまうので、そのままgitで扱うとすべてのファイルが実行可能権限を持ったなんとも危なっかしい構成になってしまいます。

### 対策

<pre class="lang:sh decode:true " >$ git config core.filemode false</pre>

で`filemode`の変更を無視するように設定しておきましょう。

### 参考

[Windows Git users: Please check your core.fileMode setting &#8211; Google グループ][1]

