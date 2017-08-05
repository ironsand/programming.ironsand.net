---
title: xampp で mod_rewrite を使う方法
author: 鉄
type: post
date: 2012-01-05T11:16:06+00:00
url: /2012/how-to-use-mod_rewrite-in-xampp/
categories:
  - Apache
  - xampp

---
見た目が素敵なURLに変えるための mod_rewrite を xampp で使う方法を解説します。

### mod_rewriteでできること

ここに検索でたどり着いた人は Apacheのモジュール mod_rewrite で何ができるかはしってると思いますが念のために例を上げておくと

`http://localhost/index.php?user=foo&name=bar`

と書く所を

`http://localhost/foo/bar.html`

と書ける機能です。

**foo/bar.html** にアクセスすると内部で
  
**index.php?user=foo&name=bar** が呼び出されるわけです。

### Xamppの設定方法

xampp は既にインストールして使ってる前提で話を進めますのでインストールがまだの方はインストールしてからまた来てください。

1. まずApacheの設定ファイル http.conf を開きます。
  
自分の環境では[ X:\sugarsync\bin\**xampp\apache\conf\httpd.conf** ] にありました。

2. モジュールがコメントアウトされてないか確認する

<pre>#LoadModule rewrite_module modules/mod_rewrite.so</pre>

のようになってたら **&#8220;#&#8221; を取って**

<pre>#LoadModule rewrite_module modules/mod_rewrite.so</pre>

とします。

3. リライトの規則を書く。
  
http.conf にどう表示を転送(書き換え？)するか RewriteRule を記述します。

<pre>&lt;IfModule rewrite_module&gt;
# bar.htmlを作りドキュメントルートに置いて
# http://localhost/foo.html でアクセスできるか確認しましょう。
RewriteEngine On
RewriteRule /foo.html /bar.html
&lt;/IfModule&gt;</pre>

4. xampp を再起動 で完了
  
http://localhost/foo.html にアクセスして bar.html の内容が表示されればOK！

### それでも動かない場合

…とここまではGoogleで [Xampp mod_rewrite] で検索すると解説されてるサイトいっぱい出てきたんですが上記の設定だけではうちの環境では動きませんでした。

色々調べてると

<pre>&lt;Directory /&gt;
    Options All
&lt;/Directory&gt;</pre>

するといいよー。

的な記述をみつけたので

<pre>&lt;Directory /&gt;
    Options FollowSymLinks
    AllowOverride None
    Order deny,allow
    Deny from all
&lt;/Directory&gt;</pre>

を

<pre>&lt;Directory /&gt;
    Options <b>All</b>
    AllowOverride None
    Order deny,allow
    Deny from all
&lt;/Directory&gt;</pre>

に書き換えてみたけどダメ。

何が悪いのかわからないので、そのまま httpd.conf を眺めたら

<pre>&lt;Directory "X:/sugarsync/bin/xampp/htdocs"&gt;
    (略)
    Options Indexes FollowSymLinks Includes ExecCGI
    (略)
&lt;/Directory&gt;</pre>

な所を見つけたので、これを

<pre>&lt;Directory "X:/sugarsync/bin/xampp/htdocs"&gt;
    (略)
    <b>#</b>Options Indexes FollowSymLinks Includes ExecCGI
    <b>Options All</b>
    (略)
&lt;/Directory&gt;</pre>

に変えて xampp を再起動させたら……動いたーー！！！

### 動的ページを静的なページ風に出力

最初に上げた例のような動作をするためのRewriteRuleの設定は

<pre>RewriteRule /([0-9A-Za-z]+)/([0-9A-Za-z)]+).html$ /index.php?user=$1&name=$2</pre>

ただ、こうすると index.php の中で相対パスの画像などを呼び出していると
  
http://localhost/img/01.jpg を呼びたいのに http://localhost/foo/img/01.jpg を参照してしまう問題が発生してしまいますので画像などの参照は全て絶対パスを記述するか、もしくは

<pre>RewriteRule /([0-9A-Za-z]+)-([0-9A-Za-z)]+).html$ /index.php?user=$1&name=$2</pre>

こうして
  
http://localhost/foo/bar.html の代わりに
  
http://localhost/foo-bar.html で我慢するという方法があります。

ただこの方法の場合は引数に&#8221;-&#8220;を入れると意図しない動作になりますのでその点に注意しないといけませんが。

mod_rewrite は他にも色々と細かい設定ができますので更に知りたい方は参考のページを見るか検索で何か良さげなページを探してください。

### 参考

mod_rewrite
  
<http://tech.bayashi.net/svr/doc/apache/mod_rewrite.html>

mod_rewrite サンプル集/楽
  
<http://tech.bayashi.jp/archives/entry/techweb/2007/001981.html>

Apache : mod_rewriteリファレンス &#8211; dawgsdk.org
  
<http://blog.dawgsdk.org/weblog/archives/411011>

Enable mod_rewrite in windows , WAMP, XAMPP
  
<http://phpcollection.com/mod-rewrite-windows-wamp-xampp/>

