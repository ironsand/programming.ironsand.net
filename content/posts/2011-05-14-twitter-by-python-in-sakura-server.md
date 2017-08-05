---
title: さくらのレンタルサーバーでPythonのTwitterライブラリを使う
author: 鉄
type: post
date: 2011-05-14T01:04:54+00:00
url: /2011/twitter-by-python-in-sakura-server/
categories:
  - python

---
### はじめに

最初に書いておきます。 SSH でログインした telnet 上ではTwitterのつぶやきが行えることを確認しましたが cron で動かしたり、CGIから呼び出したりはうまくいってません。 その情報がほしい方は他のサイトへどうぞ。 情報をすでに持っている方はぜひ教えてください。

～～～～～～～～前置きここまで～～～～～～～～

Twitterの投稿をPythonを使ってさくらのレンタルサーバで行いたいけども外部モジュールである simplejson や twitter をインストールしないと動かずに<pre class=prettyprint>ImportError: No module named simplejson</pre> 

やら<pre class=prettyprint>ImportError: No module named twitter</pre> 

なんかのエラーが出てしまう。

### インストールに必要なもの

外部モジュールを使うためには以下の物が必要になってくる。

  1. 外部モジュールのファイル本体
  2. さくらのレンタルサーバーのスタンダード以上のプラン
  3. FTPクライアント
  4. telnet/SSH クライアント

**外部モジュールのファイル本体**
  
使いたい外部モジュールのファイルをダウンロードしてサーバーにあげて置かなければいけません。
  
今回は python-twitter とその依存関係のファイル。

**さくらのレンタルサーバーのスタンダード以上のプラン**
  
スタンダード以上のプランでないと telnet/SSH が使えないのでライトプランの人は諦めてください。(ノД\`)/~ サヨーナラ

**FTPクライアント**
  
なくてもできるんですが、あったほうが便利なので。
  
現在使ってるのがなければFFFTPを使っておいてください。

**telnet/SSH クライアント**
  
次に telnet クライアント。 これも何使っても構わないんですが、既に使ってる別のがないのであればフリーの「<a href=http://yebisuya.dip.jp/Software/PuTTY/>PuTTY ごった煮版</a>」を使いましょう。

### 必要なモジュールファイルのダウンロード

&#8220;python-twitter-0.8.1.tar.gz&#8221;
  
<http://code.google.com/p/python-twitter/>

だけをインストールするで良いなら楽なんですが、依存関係が3つあるって上のサイトに書いてますので、指定された

&#8220;httplib2-0.6.0.tar.gz&#8221; と
  
<http://code.google.com/p/httplib2/>

&#8220;simplejson-2.1.5.tar.gz&#8221; と
  
<http://pypi.python.org/pypi/simplejson>

&#8220;simplegeo-python-oauth2-debian-1.5.169-0-gaee5557.tar.gz&#8221; を
  
<http://github.com/simplegeo/python-oauth2>

ダウンロードしてきてFTPクライアントを使ってサーバーにアップロードします。ファイルを展開してからアップロードしても良いんですが、そうすると転送時間が結構かかっちゃうのでtelnet上で展開することにします。

FTPクライアントでファイルのアップロード問題ないでしょうから説明を飛ばします。ホームディレクトリの直下にtempとか適当なフォルダを作ってそこに上げておいてください。

### PuTTYの使い方

PuTTYのインストールが終わったらputty.exeを起動して設定画で[Session]の中にある Host Name (or IP address) に [username].sakura.ne.jp を入力して、それから Port を &#8220;22&#8221; に設定します。

設定を入力したら[Open]で telnet を開いて<pre class=prettyprint>login as:</pre> 

でユーザー名とパスワードを入力します。 ユーザー名に .sakura.ne.jp 部分は**いりません。**

ログインできたらちゃんと動いてるか確認するためにpythonのバージョンの確認をしておきましょう。<pre class=prettyprint>%python --version Python 2.6.2</pre> 

あと作業時に環境変数PYTHONPATHを設定しておかないとうまくいかないで、<pre class=prettyprint>setenv PYTHONPATH ~/lib/python</pre> 

でsetenv PYTHONPATH ~/lib/python で設定しておきます。

次にさっきアップロードしたファイルを展開します。 tempフォルダを作ったので<pre class=prettyprint>%cd temp</pre> 

でカレントディレクトリを変更して、<pre class=prettyprint>%tar zxvf simplejson-2.1.5.tar.gz</pre> 

を4回繰り返して全部展開します。 ファイル名は数文字入力してTABキーを押せば補完されます。

解凍できたら展開されたディレクトリに入って<pre class=prettyprint>%python setup.py install --home=~</pre> 

と入力します。これを4回繰り返すわけですが、依存関係があるので
  
C:\python-twitter-0.8.1>python setup.py build
  
C:\python-twitter-0.8.1>python setup.py install

httplib2 → simplejson → simplegeo → python-twitter

の順で行ってください。

最後にちゃんとインストールで来たか import で確認しておきます。<pre class=prettyprint>%python >>>import twitter >>>exit()</pre> 

エラーが出てこなければ成功です。

### 参考にしたサイト

「さくらのレンタルサーバ」で Python 外部モジュールを使う　改訂版
  
<http://www.emptypage.jp/notes/pymods-on-sakura.html>

Python Twitter のインストール
  
<http://www.yukun.info/blog/2011/03/python-twitter-install.html>

Twitter Bot を作ってみる
  
<http://lazycozysblog.blogspot.com/2010/03/twitter-bot.html>

