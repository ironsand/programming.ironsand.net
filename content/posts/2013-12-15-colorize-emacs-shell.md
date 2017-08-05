---
title: Emacsの`M-x shell` に色を付ける
author: 鉄
type: post
date: 2013-12-15T13:53:57+00:00
url: /2013/colorize-emacs-shell/
categories:
  - Editor
  - Emacs

---
<pre class="lang:lisp decode:true " title="~/.emacs.d/inits/00-common-conf.el" >(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on)</pre>

でOK。ちなみに `M-x eshell` で高機能なシェルがつかえるらしくそちらでも色がついてた。

