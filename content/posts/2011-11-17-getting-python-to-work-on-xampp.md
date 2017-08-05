---
title: xamppでpythonを使う
author: 鉄
type: post
date: 2011-11-16T16:00:03+00:00
url: /2011/getting-python-to-work-on-xampp/
categories:
  - python
  - xampp

---
xamppには標準でpythonが入っているけど残念ながらpythonが入ってないので使いたかったら自分で入れる必要があるらしい。なので入れてみた。

### 環境

Windows 7 32bit
  
Xampp 1.7.7
  
Python 2.6.1 (Portable)

### 必要なもの

&#8220;Xampp python&#8221;で検索するとmod\_pythonの情報が出てきてインストール方法も色々と出てくるんだけれどもmod\_pythonのwindows版はpythonのバージョンが2.5までにしか対応してないようで非常にめんどくさそう。

色々探してたら簡単な方法を載せてるサイトが見つかったのでその方法を紹介します。
  
**インストールが必要な物は何もなし**。ヽ(´▽｀)ノ

### 設定方法

まず
  
[xamppをインストールしたディレクトリ]\apache\conf\httpd.conf
  
を開いて

<pre>#
# For Python
#
AddHandler cgi-script .py
ScriptInterpreterSource Registry-Strict</pre>

と追記します。

場所は多分どこでもいいけど、既に
  
&#8220;AddHandler cgi-script .cgi .pl .asp&#8221;って書いてる所があるのでその下にでも。

んで、動かしたいpythonスクリプトの行頭に

<pre>#!P:\Dropbox\bin\Python26\App\python.exe</pre>

とpython.exeがある場所を書いておきます。

以上で終わり。

### 確認

<pre>#![python.exeの置いてる場所]\python.exe
print "Content-Type: text/plain"
print
print "hello world."</pre>

と書いて[xamppのフォルダ]\htdocs\pythontest.py に保存して

xampp_start.exe でサーバーを起動させて

http://localhost/pythontext.py

を開いて &#8220;hello world.&#8221;が表示されたらOK。
  
サーバーが起動してる状態で設定したらxamppを一回終了させて再起動させないと動きません。

### やっとくと便利なこと

http://localhost/index.html が
  
http://localhost/ でも開けるように

http://localhost/index.py が
  
http://localhost/ でも開けるように設定しときましょう。

<pre>#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
&lt;IfModule dir_module&gt;
    DirectoryIndex index.php index.php4 index.php3 index.cgi index.pl index.html index.htm index.shtml index.phtml index.py
&lt;/IfModule&gt;</pre>

### 参考

Getting python to work on Xampp
  
http://www.macouno.com/2010/03/17/getting-python-to-work-on-xampp/

