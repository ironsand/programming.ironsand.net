---
title: NHK語学のラジオ講座をさくらのVPSで自動ダウンロード その2
author: 鉄
type: post
date: 2012-06-06T05:08:52+00:00
url: /2012/upload-mp3-file-to-sugarsync-by-sakura-vps/
categories:
  - ruby
  - さくらのVPS

---
前回の記事の続きです。

NHK語学のラジオ講座をさくらのVPSで自動ダウンロード
  
<http://programming.ironsand.net/2012/auto-download-nhk-language-mp3-by-vps/>

今回は**さくらVPSにダウンロードしたmp3をSugarsyncにアップロードする**について解説します。

さくらのVPS上にSugarSyncやDropboxを常駐させるのはできるのかどうかわかりませんでしたし、できてもメモリを食いそうなので今回はSugarSyncが提供するAPIを使用します。

自動的にSugarSyncにファイルをアップロードさせるための手順は以下の流れになります。

1. APIを使うためにSugarSyncのDeveloperに登録
  
2. upload_nhkradio.rb の設定
  
3. cronの設定

### 1. APIを使うためにSugarSyncのDeveloperに登録

まずSugarSyncのAPIを使うためにDeveloperとして登録を行います。
  
<http://www.sugarsync.com/developer/signup>

もしSugarsyncのアカウント自体を持ってない方がいたら、まず[こちら][1]からSugarSync自体のアカウントを作ってください。

Developer登録をすると <span style="color:red;">Access Key ID</span> と <span style="color:red;">Private Access Key</span> が手に入りますのでメモっていてください。あとで必要になります。

次に[Create App]から新しいアプリの登録を行いアプリケーションキーを取得してください。

新しいアプリの作成には以下の5つの情報を入力する必要があります。

Name:[アプリ名]&#8221;NHK Radio Uploader&#8221;とか適当に
  
Publisher:[製作者] #名前をいれておきましょう。
  
Description:[詳細] &#8220;Upload NHK radio mp3&#8221; とでも。
  
Support URL:[作者サイト] 自分はTwitterのアカウントいれてます。
  
Support Email:[連絡先] 普通に自分のメールアドレスを。

以上でAppが作れたら <span style="color:red;">App ID</span> が入手できますのでコレもメモっておいてください。

### 2. upload_nhkradio.rb の設定

必要な情報が揃いましたので upload_nhkradio.rb の設定を行います。

まず[upload_nhkradio.zip][2]をダウンロードして解凍し、**sugarsync.rb, upload\_nhkradio.rb, upload\_nhkradio_ini.rb**の3つのファイルを取り出してください。

そしてupload\_nhkradio\_ini.rbを開いて先ほど入手した情報とアップロードするフォルダ名を設定します。

    #SugarSyncのユーザ名(メールアドレス),パスワード
    @username = ""
    @password = ""
    
    #App ID /sc/などから始まる英数字
    @application = ""
    
    @access_key_id = ""
    @private_access_key = ""
    
    #refresh_tokenを設定しておけばusername, passwordはいりません。
    #username,passwordで接続すると無駄に一つ多く接続するのでrefresh_tokenを設定して使いましょう。
    @refresh_token = ""
    
    #SugarSyncのどのフォルダにアップロードするか。 e.g. "sugarsync/nhklang"
    #事前にフォルダは作っておきましょう。
    @folder_name = ""

設定がおわったら3つのファイルを前回の記事で作成したCaptureStream.rbが置いてあるnhklangディレクトリにWinSCPなどでアップロードします。

これでアップロードする準備は整いました。

`$ruby upload_nhkrandio.rb`

とするだけでアップロードが開始されるはずです。(時間が掛かるので注意)

### 3. cronの設定

ここまで来れば後は前回設定したcronに少し設定を加えるだけです。

    crontab -e

してcronの設定を開き

でcronの設定ファイルを開いて

    PATH=/etc:/bin:/sbin:/usr/bin:/usr/sbin:~/bin
    0 11 * * mon ruby ~/nhklang/CaptureStream.rb >> ~/nhklang/Capture.log
    <span style="color:red;">30 11 * * mon cd ~/nhklang; ruby upload_nhkradio.rb >> Capture.log</span></pre>
    <p></p>
    
    
    の1行を加えて全ての設定は終了です。
    
    
    これで来週から月曜日の12時頃にはパソコンのローカルフォルダに自動的に語学講座のmp3がダウンロードされてるはずです。
    
    
    <table  border="0" cellpadding="5">
      <tr>
        <td colspan="2">
          <a href="http://www.amazon.co.jp/exec/obidos/ASIN/B001AW0B0Q/ironsand0b-22/" target="_top">リトル・チャロ ~ニューヨーク編~ Vol.1 ロスト・イン・ニューヨーク [DVD]</a>
        </td>
        
      </tr>
      
      
      <tr>
        <td valign="top">
          <a href="http://www.amazon.co.jp/exec/obidos/ASIN/B001AW0B0Q/ironsand0b-22/" target="_top"><img src="http://ecx.images-amazon.com/images/I/519FZimsh7L._SL160_.jpg" border="0" alt="リトル・チャロ ~ニューヨーク編~ Vol.1 ロスト・イン・ニューヨーク [DVD]" /></a>
        </td>
        
        
        <td valign="top">
          <font size="-1"><br />NHKエンタープライズ  2008-09-26<br />売り上げランキング : 14644</p>
          
          
          <p>
            <a href="http://www.amazon.co.jp/exec/obidos/ASIN/B001AW0B0Q/ironsand0b-22/" target="_top">Amazonで詳しく見る</a></font><font size="-2"> by <a href="http://www.goodpic.com/mt/aws/index.html" >G-Tools</a></font></td>
            </tr>
            </table>
            
            
            