---
title: コマンドプロンプトを管理者権限で実行する簡単な方法
author: 鉄
type: post
date: 2012-05-15T08:34:51+00:00
url: /2012/run-a-cmd-as-admin/
categories:
  - Windows
  - Windows7

---
Windows7でハードディスクをヤフオクに出すためにチェックディスクをしようと思ったら

> chkdsk d:
  
> 十分な特権がないので、アクセスは拒否されました。
  
> 管理者特権モードで実行しているこのユーティリティを呼び出す必要があります。

と文句を言われてしまいました。

管理者権限で実行するにはデスクトップにでもショートカットを作って、プロパティから「管理者として実行」あたりにチェックを入れれば解決ですが、それさえも面倒臭い。

コンピュータの修理を頼まれて他人のパソコンで使いたい時もあるので、もっとも簡単な方法を紹介します。

### ここまで前置き

スタートボタンの「プログラムとファイルの検索」に

&#8220;cmd&#8221; と打てば cmd.exe がフィルタリングされますので、そこで

**Ctrl+Shift+Enterで実行**します。

これで管理者権限で実行できます。ショートカットさえ覚えておけば初期状態のWindows7で使えるので便利ですね。

### 参考

Run a Command as Administrator from the Windows 7 / Vista Run box
  
<http://www.howtogeek.com/howto/windows-vista/run-a-command-as-administrator-from-the-windows-vista-run-box/>

