---
title: coffee script を Emacs の smart compile を使ってjsの出力結果を出す
author: 鉄
type: post
date: 2013-12-17T15:37:33+00:00
url: /2013/coffee-script-with-smart-compile/
categories:
  - coffee
  - Editor
  - Emacs
  - javascript

---
Railsのプロジェクトで coffee script を使うけどもコンパイルは全て Asset pipelineがやってくれるので、たまに変換結果の js をちょっと見てみたい時に困った事になります。

なのでEmacsの smart compile の機能を使ってすぐに 出力結果を得られるようにしてみました。

### 解決策

`coffee -p`で標準出力に変換結果を出力してくれるので

<pre class="lang:lisp decode:true " title="~/.emacs.d/inits/30-smart-compile.el" >(global-set-key (kbd "C-c C-x") 'smart-compile)
(setq smart-compile-alist
      (append
       '(("\\.rb$" . "ruby %f"))
       '(("\\.php$" . "php %f"))
       '(("\\.coffee$" . "coffee -p %f"))       
       '(("\Gemfile$" . "bundle install"))
       smart-compile-alist))
</pre>

としておけばOKです。

### 参考

[Convert coffee to javascript and show the result to standard output in Emacs &#8211; Stack Overflow][1]

