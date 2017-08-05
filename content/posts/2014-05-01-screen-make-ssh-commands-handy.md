---
title: screenを使ってssh経由のコマンドを便利に
author: 鉄
type: post
date: 2014-04-30T21:23:03+00:00
url: /2014/screen-make-ssh-commands-handy/
categories:
  - fg
  - screen
  - ssh

---
`ssh`でログインして処理の重たいコマンドを実行した後にセッションが途切れてしまうとそのコマンドをもう一度`fb`などでフォアグラウンドに持ってこようと思っても残念ながらできません。違うシェルのインスタンスから立ち上げたらプロセスは別のインスタンスのシェルには持ってこれないかららしいです。

### Screenの使い方

まず初めからコマンドを`screen`を使って立ち上げておきましょう。

`$ screen ruby it_takes_very_long.rb`

そして、一旦`ssh`の接続を切って繋ぎ直します。

`$ screen -list`をするとこんな感じで表示されるので

    There is a screen on:
        31744.pts-0.Sakura  (Detached)
    1 Socket in /var/run/screen/S-ironsand.
    

`$ screen -r 31744.pts-0.Sakura`でスクリーンに繋ぎ直せば画面への出力をもう一度見ることが出来ます。

### 参考

[Linux Screen Tutorial &#8211; YouTube][1]

