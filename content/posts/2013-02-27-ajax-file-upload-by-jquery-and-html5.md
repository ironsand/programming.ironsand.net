---
title: JqueryとHTML5でajaxなファイルのアップロード
author: 鉄
type: post
date: 2013-02-27T09:16:07+00:00
url: /2013/ajax-file-upload-by-jquery-and-html5/
categories:
  - javascript
  - jQuery
  - ruby

---
画面遷移無しでファイルのアップロードしようと思ったらiframeを使った技とかややこしい情報が色々出てきて、なかなかやりたいことに辿りつけなかったのでメモ。

### やりたい事と条件

・ajaxなテキストファイルのアップロード
  
・テキストをRubyで編集して返す
  
・画面遷移せずに結果を表示
  
・IEは諦める。

### 必要最低限のコード

まずHTMLを用意

**ajaxupload.html**
  
`</p>
<pre><html><br>
  <head><br>
    <meta http-equiv="content-type" content="text/html;charset=utf-8"><br>
    <script type="text/javascript" src="jquery-1.7.min.js" charset="utf8"></script><br>
    <script type="text/javascript" src="ajaxupload.js" charset="utf8"></script><br>
  </head><br>
  <style>textarea{height:80%;width:100%;}</style><br>
  <body><br>
    <input type=file id=file /><br>
    <input type=button id=upload value="upload"><br><br>
    <textarea id=output></textarea><br>
  </body><br>
</html><br>
</pre>
<p>`

つぎにjavascript

**ajaxupload.js**
  
`</p>
<pre>$(function(){
  $("#upload").click(function(){
    var file = $("#file")[0].files[0];
    var reader = new FileReader();
    reader.readAsText(file, 'UTF-8');
    reader.onload = showFile;
  });
  function showFile(event) {
    $.ajax({
    type: "POST",
    url: "ajaxupload.rb",
    data: { filedata:event.target.result}
    }).done(function(msg) {
      $("#output").html(msg);
    });
  }
});
</pre>
<p>`

んで何か処理をするRubyのスクリプト。ここではファイルの中身をそのまま返してるだけ。(パス名は適宜変更してください。)
  
**ajaxupload.rb**
  
`</p>
<pre>#!P:\Dropbox\bin\RailsPortable\App\Rails\bin\ruby.exe
require "cgi"
cgi = CGI.new
print "Content-Type: text/html\n\n"
print cgi['filedata'][0]</pre>
<p>`

### デモ

サンプルを置いておきます。(さくらのレンタルサーバーはRubyの拡張子がrbではなくcgiじゃなくと動かなかったのでファイル名を変えています。

<http://ironsand.net/misc/ajaxupload/ajaxupload.html>

<a href=http://ironsand.net/misc/ajaxupload/ajaxupload.zip>上のコードをZIPで固めた奴</a>

