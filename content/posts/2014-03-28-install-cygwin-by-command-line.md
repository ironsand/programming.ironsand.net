---
title: cygwinのインストールをコマンドラインで一発で行う
author: 鉄
type: post
date: 2014-03-28T12:13:33+00:00
url: /2014/install-cygwin-by-command-line/
categories:
  - Windows
  - Windows7

---
一度`cygwin`をインストールした後なら`aptcyg`とか`cygapt`とか「あれどっちだっけ？」となる`apt`風味のインターフェースがあるんですが、初回インストール時の方法があまりなかったので書いておきます。

### インストール方法

`setup-x86_64.exe --no-admin -l %USERPROFILE%\cyg\package -P wget,ssh,rsync --download -s ftp://ftp.iij.ad.jp/pub/cygwin/ -q --root %USERPROFILE%\cyg`

これで`c:\Uers\ironsand\cyg`配下に`wget`,`ssh`,`rsync`が入ります。32bit版でも引数の取り方は変わりません。

