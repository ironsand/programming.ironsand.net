---
title: Rubyのスクリプトをサービスとして常駐させる
author: 鉄
type: post
date: 2011-05-07T11:46:31+00:00
url: /2011/how-to-run-ruby-script-as-a-deamon/
categories:
  - ruby
tags:
  - Windows
  - デーモン
  - 常駐

---
PythonかRubyのスクリプトを常駐させたかったので調べてみたらRubyの方が簡単そうだったので試してみた。

### 環境

OS:Windows 7
  
ruby 1.8.6 (2007-09-24 patchlevel 111) [i386-mswin32]
  
gem 1.3.4

Portableバージョンを使ってます。

### Win32-Serviceのインストール<pre class=prettyprint>C:\>gem install win32-service</pre> 

するだけです。 

ただうちの環境ではこんなエラーが出てしまいました。<pre class=prettyprint>P:/Dropbox/bin/RailsPortable/App/Rails/bin/ruby.exe extconf.rb checking for strncpy\_s()... yes creating Makefile nmake Microsoft(R) Program Maintenance Utility Version 9.00.21022.08 Copyright (C) Microsoft Corporation. All rights reserved. P:\Dropbox\bin\RailsPortable\App\Rails\bin\ruby -e "puts 'EXPORTS', 'Init\_api'" > api-i386-mswin32.def cl -nologo -I. -I. -IP:/Dropbox/bin/RailsPortable/App/Rails/lib/ruby/1.8/i386-mswin32 -I. -MD -Zi -O2b2xg- -G6 -DHAVE\_STRNCPY\_S -c -Tcwin32/api.c cl : コマンド ライン warning D9035 : オプション 'Og-' の使用は現在推奨されていません。今後のバージョンからは削除されます。 cl : コマンド ライン warning D9002 : 不明なオプション '-G6' を無視します api.c p:\dropbox\bin\railsportable\app\rails\lib\ruby\1.8\i386-mswin32\config.h(2) : fatal error C1189: #error : MSC version unmatch NMAKE : fatal error U1077: '"C:\Program Files\Microsoft Visual Studio 9.0\VC\bin\cl.EXE"' : Stop.</pre> 

うわー、意味ワカンネー。

それっぽい所にある &#8220;MSC version unmatch&#8221; でぐぐってみると、このエラーは使っているコンパイラがruby本体に使われたものと違ったら起きるものらしい。

本当はruby本体に使われたコンパイラを調べて、それと同じものを用意しないといけないけども、「コンパイラが新しい分には大丈夫だろ」と言う事で

<pre>P:\Dropbox\bin\RailsPortable\App\Rails\lib\ruby\1.8\i386-mswin32\config.h</pre>

にある config.h をひらいて

<pre>#if _MSC_VER != 1200
#error MSC version unmatch
#endif</pre>

を

<pre>#if _MSC_VER &lt; 1200
#error MSC version unmatch
#endif</pre>

に修正。直してからもう一度<pre class=prettyprint>C:\>gem install win32-service</pre> 

すればインストールが最後まで終わりました。

### 実際にサービスで動かせるか確認

実際にデーモン化できるかどうかを確認するために以下のスクリプトをコピペして好きな場所に好きな名前で保存。

俺は P:\Dropbox\servicetest.rb に保存しました。<pre class=prettyprint>require 'rubygems' require 'win32/daemon' include Win32 class Daemon def service\_main while running? sleep 3 File.open("c:\\test.log", "a"){ |f| f.puts "service is running" } end end def service\_stop exit! end end Daemon.mainloop</pre> 

てっきりこれを

<pre>P:\Dropbox>ruby servicetest.rb</pre>

すれば良いと思ったのに、やってみると

<pre>in `mainloop': Service_Main thread exited abnormally (Win32::Daemon::Error)</pre>

なエラーが帰ってきてしまいました。

サービスとして使うために、事前にサービスとして登録しないと動かないらしいので

<pre>C:\Users\tetsuya>sc create rubyservice binPath= "p:\Dropbox\bin\RailsPortable\App\Rails\bin\ruby p:\Dropbox\servicetest.rb" type= own start= auto
[SC] CreateService SUCCESS</pre>

"rubyservice"になってるサービス名は何でも良いです、適当に好きな名前にしてください。binPath で指定するruby.exe の場所とサービス化したい .rb ファイルの場所はフルパスで記入してください。 <b style=color:#d00;>PATHを通してても無視されます。</b>

サービスが登録されたら起動します。

<pre>C:\Users\tetsuya>sc start rubyservice

SERVICE_NAME: rubyservice
        TYPE               : 10  WIN32_OWN_PROCESS
        STATE              : 4  RUNNING
                                (STOPPABLE, PAUSABLE, ACCEPTS_SHUTDOWN)
        WIN32_EXIT_CODE    : 0  (0x0)
        SERVICE_EXIT_CODE  : 0  (0x0)
        CHECKPOINT         : 0x0
        WAIT_HINT          : 0x0
        PID                : 5868
        FLAGS              :
</pre>

上手くいってたら、これで3秒毎に "C:\test.log" に "service is running" と書き込み続けるサービスが作成されているはずです。

このまま放置しとくと邪魔なので、使わないサービスは

<pre>C:\Users\tetsuya>sc delete rubyservice
[SC] DeleteService SUCCESS</pre>

で削除しておきましょう。次回Windows起動時に削除されます。<div style=color:red;>require 'rubygems' が抜けてしまっていたので追記</div> 

### 参考サイト

Win32-Serviceが欲しかったのでRubyGemsをインストール
  
<http://projectzero-swb.blogspot.com/2009/08/win32-servicerubygems.html>

RubyでWindowsのサービスを作る
  
<http://projectzero-swb.blogspot.com/2009/08/rubywindows.html>

[ruby] Windowsでgem install jsonでエラー
  
<http://www.pistolfly.jp/weblog/2008/03/windowsgem-install-json.html>

File: daemon.txt
  
<http://rubyforge.org/docman/view.php/85/596/daemon.html>

