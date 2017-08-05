---
title: さくらのVPSにneroAacEncをインストールしてmp3をm4aに変換する
author: 鉄
type: post
date: 2013-03-12T04:27:25+00:00
url: /2013/encode-mp3-m4a-aac-in-sakura-vps/
categories:
  - さくらのVPS
tags:
  - aac
  - ffmpeg
  - m4a
  - neroaac

---
### 作業目的

さくらのVPSで自動ダウンロードしてるNHKの語学講座が大量になってきて容量が馬鹿にならなくなってきたので
  
mp3で出力されたものをm4aに変換しようとNeroAAC Encoderのインストール作業メモ。

### インストール方法

まず

コマンドラインツールをここからダウンロードしてくる。
  
http://www.nero.com/enu/company/about-nero/nero-aac-codec.php

wgetで直接取ってくるなら
  
`$ wget http://ftp6.nero.com/tools/NeroAACCodec-1.5.1.zip`

圧縮ファイルを展開して
  
`$ unzip ~/NeroAACCodec-1.5.1.zip -d neroaac`

実行権限を付加
  
`$ chmod +x ./neroaac/linux/neroAac*`

んで、動作を確認
  
`$ ./neroaac/linux/neroAacEnc`

<pre>*************************************************************
*                                                           *
*  Nero AAC Encoder                                         *
*  Copyright 2009 Nero AG                                   *
*  All Rights Reserved Worldwide                            *
*                                                           *
*  Package build date: Feb 18 2010                          *
*  Package version:    1.5.4.0                              *
*                                                           *
*  See -help for a complete list of available parameters.   *
*                                                           *
*************************************************************

ERROR: no input file specified
</pre>

が表示されれればインストール作業は終了！

### エラーが出た時の対処

残念ながら自分の環境ではエラーが出てしまった。
  
`$ ./neroaac/linux/neroAacEnc<br />
-bash: ./neroaac/linux/neroAacEnc: /lib/ld-linux.so.2: bad ELF interpreter: そのようなファイルやディレクトリはありません`

`sudo yum install ld-linux.so.2`

してld-linux.so.2をインストールしたら今度は別のエラー。

`error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory`

libstdc++.so.6を

`$ sudo yum install libstdc++.so.6`

で持ってこようとすると、複数バージョンがあるから選べって言われる。

`Error: Protected multilib versions: libstdc++-4.4.7-3.el6.i686 != libstdc++-4.4.6-4.el6.x86_64<br />
 You could try using --skip-broken to work around the problem<br />
 You could try running: rpm -Va --nofiles --nodigest`

`$ sudo yum install libstdc++`

で呼べばいいらしい。よくわからーん！
  
なんでそのエラーメッセージで対処法がこうなるんだろう…？

んで、これだけだとだめでこの後に

`$ sudo yum install libstdc++.so.6`

を呼べば上手くいった。つまりやったことは

`$ sudo yum install ld-linux.so.2<br />
$ sudo yum install libstdc++<br />
$ sudo yum install libstdc++.so.6`

の3つ。

### やっと動いた

<pre>[ironsand@www9181ue linux]$ ./neroAacEnc
*************************************************************
*                                                           *
*  Nero AAC Encoder                                         *
*  Copyright 2009 Nero AG                                   *
*  All Rights Reserved Worldwide                            *
*                                                           *
*  Package build date: Feb 18 2010                          *
*  Package version:    1.5.4.0                              *
*                                                           *
*  See -help for a complete list of available parameters.   *
*                                                           *
*************************************************************</pre>

あとは /usr/local/bin にでも移動して終了。インストールしたユーザーしか使わないなら必要なし。

### neroAacEncの使い方

基本的な使い方は

`neroAacEnc.exe -br 32000 -if input_file.wav -of output_file.m4a`
  
32kb/sのm4aファイルに変換。

neroAacEncはwavファイルしかインプットに使えないので
  
ffmpegでmp3をwavに変換して、それをpipeでそのままneroAacEncに渡す場合はこう。

`$ ffmpeg -i input_file.mp3 -acodec pcm_s32le -ac 1 -f wav - | neroAacEnc -if - -br 32000 -ignorelength -of output_file.m4a`

-acは 音声のchなので適宜変える。

### 結果

これだけ頑張ってインストールしたけども、NHKのラジオ音声をコレ以上ビットレート下げるとハッキリとわかるぐらいに音声が劣化したので自動変換するのはやめておいた。

悲しいけど、まあいつか使うことがあるかも知れないと思い込むことにしよう…。

### 参考

Nero AAC Encoder をLinux (Ubuntu)で使えるようにする手順メモ | 銀メモ -SilveryMemo-
  
<http://silverymemo.wordpress.com/2012/01/07/article-2329/>

decode 5.1 audio with ffmpeg and pipe to neroaacenc ? [Archive] &#8211; Doom9&apos;s Forum
  
<http://forum.doom9.org/archive/index.php/t-141723.html>

