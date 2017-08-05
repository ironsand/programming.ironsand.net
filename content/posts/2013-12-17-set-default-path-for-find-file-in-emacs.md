---
title: Emacsの`find-file`で開くデフォルトのパスを変更する
author: 鉄
type: post
date: 2013-12-17T12:36:01+00:00
url: /2013/set-default-path-for-find-file-in-emacs/
categories:
  - Editor
  - Emacs

---
何故かMacのOSを最新の Mavericks(10.9.1)に変えたらEmacsの `C-x C-f` で表示されるデフォルトのパスが ルートの `/` に変わってしまったのでその対策。

### 対策法

下の対策はうまく動いてませんでした。homebrewの最新版だと対応されてるらしいので `homebrew install --cocoa emacs`で homebrewから入れたら解決します。

<del datetime="2013-12-21T01:32:47+00:00">Emacsの設定に <code>default-directory</code> を追加したらOK</p> 


  <p>
    <span class="lang:lisp decode:true  crayon-inline " >(setq default-directory &#8220;~/&#8221;)</span>
  </p>



  <h3>
    参考
  </h3>



  <p>
    <a href="http://stackoverflow.com/questions/6464003/emacs-find-file-default-path">settings &#8211; emacs "Find File:" default path &#8211; Stack Overflow</a></del>
  </p>



  