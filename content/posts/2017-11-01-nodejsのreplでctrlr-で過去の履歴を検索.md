---
title: NodeJSのREPLでctrl+r で過去の履歴を検索
author: 鉄
type: post
date: 2017-11-01T06:28:12+00:00
url: /2017/nodejsのreplでctrlr-で過去の履歴を検索/
categories:
  - javascript
  - Node.js

---
`bash`やRubyの`pry`で`ctrl+r`で使える reverse interactive search を`node`のシェルでも使う方法の紹介です。

### rlwrap のインストール

`rlwrap`が必要なので`brew install rlwrap`でインストールしましょう。他の環境の場合は環境にあったパッケージマネージャでインストールしてください。

`rlwrap`はGNUの`readline`的な振る舞いをするためのパッケージだそうです。

### node側の設定

<pre class="lang:sh decode:true " title="~/.bashrc" >alias node="NODE_NO_READLINE=1 rlwrap node"</pre>

を追加して`node`で`readline`を使うように設定しておきましょう。

### 参考

https://stackoverflow.com/questions/46714331/how-to-use-reverse-interactive-search-in-nodejs-repl
