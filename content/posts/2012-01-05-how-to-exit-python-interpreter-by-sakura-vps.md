---
title: さくらのVPSでpythonのインタプリタを終了させる
author: 鉄
type: post
date: 2012-01-05T11:51:15+00:00
url: /2012/how-to-exit-python-interpreter-by-sakura-vps/
categories:
  - python
  - さくらのVPS

---
さくらのVPSにputtyを使ってSSHでログインしてる時に間違えて /usr/bin/python を叩いてしまい(コピーしようとしたら貼りつけてしまった。)インタプリタを終了できなくてちょっと焦ったので終了方法のメモ。

&#8216;Use Ctrl-D (i.e. EOF) to exit.&#8217;

とか言ってるくるけど Ctrl-D をおしてもサーバーまで届かない。

正しい終了方法は

<pre>import sys
sys.exit()</pre>

だそうです。 ああ、そうか sys をインポートしなきゃならんのか。プログラムを書いてる時だと気づくのにインタプリタ普段使わないから何かちがうものだと勝手に思い込んじゃってたよ…。

### 参考

pythonインタプリタを終了する
  
<http://blog.justoneplanet.info/2010/08/07/python%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%97%E3%83%AA%E3%82%BF%E3%82%92%E7%B5%82%E4%BA%86%E3%81%99%E3%82%8B/>

