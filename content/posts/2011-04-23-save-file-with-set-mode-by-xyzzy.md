---
title: xyzzyでファイル保存時にmodeの変更をする
author: 鉄
type: post
date: 2011-04-23T08:23:30+00:00
url: /2011/save-file-with-set-mode-by-xyzzy/
categories:
  - xyzzy
tags:
  - xyzzy

---
Xyzzy上で新規作成した javascript とか ruby のバッファに毎回モード設定をするのがめんどくさかったので書いた。 siteinit.l か ~/.xyzzy のどこかに貼りつけて使ってください。

※同じ拡張子に複数のモードが紐付けられていると、古い方に設定されるようになっていたので修正<pre class=prettyprint>;ファイル保存時に拡張子をチェックして適切なモードに変更する。 ;リネーム時にしたかったけど、hookが用意されてないので断念。 (defun set-buffer-mode () (block sbm (mapcar (lambda (l) (when (string-matchp (car l) (get-buffer-file-name)) (funcall (cdr l)) (return-from sbm)) ) \*auto-mode-alist\*))) (add-hook '\*after-save-buffer-hook\* 'set-buffer-mode)</pre> 

