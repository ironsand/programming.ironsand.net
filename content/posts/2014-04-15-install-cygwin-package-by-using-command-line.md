---
title: cygwinの必要なパッケージをコマンドラインで一括インストール
author: 鉄
type: post
date: 2014-04-14T19:55:58+00:00
url: /2014/install-cygwin-package-by-using-command-line/
categories:
  - cal
  - Commands
  - curl
  - cygwin
  - git
  - rsync
  - ssh
  - tree
  - wget
  - Windows
  - zip

---
今まではcygwinをインストールしたディレクトリを全部SugarSyncで同期して使ってたんだけど、
  
よくわからないままに色々入れてたら700MBぐらいあったので整理整頓することにしました。

### どうするか？

既にインストールされてるcygwinのファイルを整理するのはめんどくさかったの新規インストールをすることにしたのはいいけど、何せパッケージ選択がめんどくさい。めんどくさいっていうか手動でやると必ず忘れてしまうので自動化したい。

そこでコマンドラインインストールの登場です！

### インストール方法

    setup-x86.exe --quiet-mode -P util-linux,curl,wget,openssh,rsync,zip,tree -s ftp://ftp.iij.ad.jp/pub/cygwin/ --root %USERPROFILE%\cyg --local-package-dir %USERPROFILE%\cyg 
    

これでホームディレクトリ直下の `C:\Users\ironsand\cyg`とかにインストールされる。

### やめたパッケージ

`gcc`とか入れてcygwinでコンパイルして色々してると毎回ドツボにハマるので、もうそういうのはVirtualBox上のUbuntuですることにする。

`ruby`や`python`はWindowsのネイティブパッケージを使う。結局なんだかんだでそれが一番安定してる気がするので。

`git`も`cygwin`用のパス名周りのエラーが鬱陶しくなることがちょくちょくあったので`Chocolatey`使って`cinst git`でインストールする方法に変更。

### 注意点

何故か 64bit バージョンは動きませんでした。理由はわかりませんが、こういう関係のソフトは32bit版のほうが今はまだ安定してる気がするし大量にメモリ使うこともないので気にしないことにします。

`ssh`だと`ssh`コマンドはインストールされないので`openssh`を指定しましょう。

インストール後に`/etc/passwd`のホームディレクトリ設定を`/home/username`から`cygdrive/c/Users/username`とWindowsのホームフォルダに変更しておくと`ssh`とかのコマンドの時に設定ファイルを自動的に読みに行ってくれるので便利。便利というかしないとちゃんと動かない。

あと環境変数に`set HOME=%USERPROFILE%`もどこかに仕込んでたほうが良いかも。

### Util-Linux

何故かカレンダー表示の`cal`コマンドが見つからなかったので探してみたら、`cal`のみのインストールはないらしい。
  
とりあえず`util-linux`が良さそうなんでこれを使う事にした。

### tree

Windows由来のコマンドなのにWindowsの`tree`コマンドは階層指定もできない残念仕様なので`cygwin`のを入れました。`tree -L 2`とかで階層指定できる。便利！

