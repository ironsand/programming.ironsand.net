---
title: Windowsでシンボリックリンクを作成するにはアドミン権限が必要です。
author: 鉄
type: post
date: 2014-03-22T00:27:55+00:00
url: /2014/you-need-to-have-privilege-to-create-symlink-in-windows/
categories:
  - Commands
  - Windows
  - Windows7

---
ホームディレクトリに直接ファイルを置くんじゃなくて、
  
必要なファイルをDropboxに置いといて同期して使おうと思ったので

`mklink ~/.nyaos p:\Dropbox\rc\.nyaos`

としたら

`この操作を実行するのに十分な特権がありません。`

と怒られた。

### なぜ権限が必要か？

「さっき自分で作ったファイルを自分のホームフォルダに移動させるのになんで権限が必要なんです！？」と不思議に思って調べてみたら、シンボリックリンクの作成に必要な`SeCreateSymbolicLinkPrivilege`が通常はユーザーが持っていないかららしい。

何故そんな謎な仕様になってるかは全くわからない。

日本語圏で検索しても「とりあえず管理者権限にしとけ」的な情報しか出てこなかったのでここに書いておきます。

### 参考

[filesystems &#8211; Using windows mklink for linking 2 files &#8211; Stack Overflow][1]

[windows 7 &#8211; Got not sufficient privileges message in CMD when logged on as administrator &#8211; Super User][2]

