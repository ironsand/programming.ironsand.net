---
title: rbenvでインストールしたgemをEmacsから使う
author: 鉄
type: post
date: 2014-01-23T08:04:42+00:00
url: /2014/how-to-use-gem-in-rbenv-with-emacs/
categories:
  - Editor
  - Emacs
  - Rails
  - ruby

---
rspec書いてる時にEmacsから簡単に呼び出せたら便利だと思って`smart-compile`の設定をこんな風に書き換えたんだけど、

<pre class="lang:lisp decode:true " >(setq smart-compile-alist
      (append
       '(("\_spec.rb$" . "rspec %f"))
       '(("\\.rb$" . "ruby %f"))
       '(("\\.php$" . "php %f"))
       '(("\\.coffee$" . "coffee -p %f"))       
       '(("\Gemfile$" . "bundle install"))
       smart-compile-alist))
</pre>

でちゃんと`Compile command: rspec foo_spec.rb`は呼び出せるものの実行すると

<pre class="lang:default decode:true " >-*- mode: compilation; default-directory: "~/dev/zombie/spec/lib/" -*-
Compilation started at Thu Jan 23 16:50:59

rspec zombie_spec.rb
/bin/bash: rspec: コマンドが見つかりません

Compilation exited abnormally with code 127 at Thu Jan 23 16:51:00</pre>

な感じでエラーになってしまう。

どうやら rbenv の環境がEmacs側で認識されてないので rbenv で入れた gem のコマンドも使えないのが原因らしい。

### 解決策

[rbenv.el][1] をインストールすれば解決しました。

<pre class="lang:default decode:true " >cd ~/.emacs.d/git
git clone https://github.com/senny/rbenv.el.git
ln -s ~/.emacs.d/git/rbenv.el/rbenv.el ../../site-lisp/</pre>

でインストールしておいて

<pre class="lang:lisp decode:true " title="~/.emacs.d/inits/10-rbenv.el" >(require 'rbenv)
(global-rbenv-mode)</pre>

しておけばOKです。

