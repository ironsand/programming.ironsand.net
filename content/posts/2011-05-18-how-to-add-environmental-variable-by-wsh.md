---
title: WSHで環境変数のPATHに値を追加する
author: 鉄
type: post
date: 2011-05-17T19:36:08+00:00
url: /2011/how-to-add-environmental-variable-by-wsh/
categories:
  - WSH

---
wshで環境変数のUserのPATHに値を追加したかったので、調べてみたらここがそれっぽいんだけど、

WSHで環境変数を設定する
  
http://www.atmarkit.co.jp/fwin2k/win2ktips/460envset/envset.html

ここで紹介されてるwsfファイルをWindows 7(32bit)環境で動かすと、UserにSystem側のPathまで全部追加されてしまった。

ExpandEnvironmentStrings(&#8220;%Path%&#8221;) を使うと全ての設定されてるパスをとってきてしまうらしい。 なので

objEnv=objShell.Environment(&#8220;USER&#8221;) としといて
  
objEnv.Item(&#8220;path&#8221;) で取得すればUserの環境変数だけが取得できるのでこっちを使うと多分良い。 WSHを普段全く触らないからホントに良いのかよくわからないけども、とりあえずうちの環境では下のコードを foo.wsf の名前で utf8n で保存してダブルクリックしたらPATHの値が更新された。 <pre class=prettyprint><?xml version="1.0" encoding="UTF-8" standalone="yes" ?> <package> <job id="environment"> <?job error="true" debug="true" ?> <object id="objFs" progid="Scripting.FileSystemObject" /> <script language="VBScript"> <![CDATA[ Set objShell=WScript.CreateObject("WScript.Shell") Set objEnv=objShell.Environment("USER") objEnv.Item("path")=objEnv.Item("path") & ";" & "C:\hoge\bin" ]]> </script> </job> </package></pre> 

重複確認なんて全くしてないので何個でも追加されるので注意してください。

