---
title: xyzzy から Rhino(javascript)を直接実行する
author: 鉄
type: post
date: 2010-03-14T18:56:16+00:00
url: /2010/xyzzyからrhino-javascriptを直接実行する/
categories:
  - xyzzy
tags:
  - javascript
  - xyzzy

---
#### xyzzyから直接javascriptを使う

今回の記事はRhinoのインストールが行われてる事と xyzzy で jscript-mode がインストールされている事が前提条件になります。 RhinoのWindowsでのインストール方法については前回の記事『[Windows(cygwin+zsh)環境でRhinoを使う][1]』を参考にしてください。 今回の記事の設定を行うと xyzzy から直接Rhinoを呼び出して下の画像のように簡単なスクリプトを気軽に書けるようになります。 

[<img src="http://programming.ironsand.net/wp-content/uploads/2010/03/xyzzy-jscript-mode-300x195.jpg" alt="" title="xyzzy-jscript-mode" width="300" height="195" class="alignnone size-medium wp-image-28" srcset="http://programming.ironsand.net/wp-content/uploads/2010/03/xyzzy-jscript-mode-300x195.jpg 300w, http://programming.ironsand.net/wp-content/uploads/2010/03/xyzzy-jscript-mode-150x97.jpg 150w, http://programming.ironsand.net/wp-content/uploads/2010/03/xyzzy-jscript-mode.jpg 805w" sizes="(max-width: 300px) 100vw, 300px" />][2]

下記のlispはruby-modeから引っ張ってきて少し修正を加えたもので、これを ~/.xyzzy や siteinitl. に貼りつければjscript-mode で C-c C-x すれば現在編集中のバッファの javascript が実行されます。<pre class=prettyprint>;;jscript-mode(for Rhino) (setf \*js-prog\* "java org.mozilla.javascript.tools.shell.Main") (setf \*js-classpath\* "X:/sugarsync/bin/rhino1\_7R2/js.jar") (defun js-run-script-immediate () (interactive) (js-run "")) (defun js-run (args) (let ((tempfile (make-temp-file-name "\_\_temp\_" "js" (default-directory)))) (write-file tempfile t nil (buffer-fileio-encoding) (buffer-eol-code)) (command-execution (concat \*js-prog\* " -f \"" tempfile "\" " args)) (delete-file tempfile :if-does-not-exist :skip))) (defun command-execution (command) (interactive "sCmmand:") (let ((proc nil)(buffer (selected-buffer))) (with-output-to-temp-buffer ("\*cmd\*" 5) (unwind-protect (setq proc (make-process command :environ \`(("CLASSPATH" . ,\*js-classpath\*)) :output(selected-buffer) :exec-directory (default-directory buffer))))) (while (eq :run (process-status proc)) (sit-for 0.05)(do-events)) (if (= 0 (point-max)) (let ((buff (selected-buffer))) (other-window) (delete-buffer buff) (delete-other-windows)) (other-window)) (message (concat " '" command "' ended.")))) (add-hook 'ed::\*jscript-mode-hook\* #'(lambda () (define-key ed::\*jscript-mode-map\* '(#\C-c #\C-x) 'js-run-script-immediate)))</pre> 

\*js-classpath\* と define-key は好みに合わせて適宜変更の事。

