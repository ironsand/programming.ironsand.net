---
title: find の `-exec` オプションを cygwin で使うときの注意点
author: 鉄
type: post
date: 2014-04-15T04:15:00+00:00
url: /2014/finds-exec-option-with-cygwin/
categories:
  - Commands
  - cygwin
  - find

---
何故動かないか結構困ったのでメモ。

### 動かないもの

    find . -name '*.mkv' -exec bash -c 'echo "{}"' \;
    

cygwin 環境、というか`cmd.exe`で`cygwin`の中の`find`コマンドを呼び出してるとこれはエラーになっちゃいます。

### 理由

何故なら`find`の`\;`の`\`は`;`をエスケープする役割なので、当然ここにはエスケープキャラクターを入れて置かなければならないわけですが、Windowsの`cmd`において`\`はパス区切りであって何もエスケープしてくれません。

なので`cygwin`の`find`を`cmd.exe`や`nyaos`などのWindows環境のシェルから使うときは`cmd.exe`のエスケープキャラクターの`^`を使ってこんなふうに書きましょう。

    find . -name '*.mkv' -exec bash -c 'echo "{}"' ^;
    

もしくはどちらの環境でも使える方法の

    find . -name '*.mkv' -exec bash -c 'echo "{}"' ';'
    

を使うのもいいかもしれません。

