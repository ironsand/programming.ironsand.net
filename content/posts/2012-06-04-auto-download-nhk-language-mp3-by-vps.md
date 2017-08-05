---
title: NHK語学のラジオ講座をさくらのVPSで自動ダウンロード
author: 鉄
type: post
date: 2012-06-04T05:41:35+00:00
url: /2012/auto-download-nhk-language-mp3-by-vps/
categories:
  - ruby
  - さくらのVPS

---
NHKラジオの語学講座を毎週ダウンロードしてるんですが、
  
外国語を勉強してるのは海外に行くためでして、海外だとダウンロードができないことがよくあります。

なのでせっかくさくらのVPSをお金払って借りてるんだから
  
勝手にダウンロードするように設定しましたので参考にどうぞ。

月曜日の12時頃には決めておいたフォルダにmp3ファイルができてます。
  
実際に先週から動かしてみてますが、こりゃ楽でいいです。
  
SugarSync にアップロードしてるので海外にいるときにiPhoneがあるだけで新しい音声を聞くことも出来ます。

記事が長くなるので今回の
  
**さくらVPSを使って自動的にNHKラジオ講座をダウンロード**

次回の
  
**さくらVPSにダウンロードしたmp3をSugarsyncにアップロードする**

の2つにわけて解説していきます。

自動的にNHKラジオ講座をダウンロードするには以下の4つの手順が必要です。

1. flvstreamerのダウンロード、コンパイル
  
2. Rubyのインストール
  
3. CaptureStream の設定
  
4. cronの設定

### 1. flvstreamerのダウンロード、コンパイル

flvstreamer をインストールするんですが、
  
まずさくらのVPSが32ビットなのか64ビットなのか確認します。

`$ cat /proc/cpuinfo | grep flags`

して値に lm が含まれていれば64bitのCPUです。

次に

`$ uname -a`

X86_64とかamd64とかが表示されたら、64ビット版のカーネルです。

64bitだとわかったので、64bitのflvstreamerをインストールしたいんですが、
  
32bitしかバイナリがおいてないので自分でコンパイルします。

    $ wget http://download.savannah.gnu.org/releases/flvstreamer/source/flvstreamer-2.1c1.tar.gz
    $ tar zxf flvstreamer-2.1c1.tar.gz
    $ cd flvstreamer
    $ make posix
    $ ./flvstreamer
    FLVStreamer v2.1c1
    (c) 2010 Andrej Stepanchuk, Howard Chu, The Flvstreamer Team; license: GPL
    ERROR: You must specify a hostname (--host) or url (-r "rtmp://host[:port]/playpath") containing a hostname

`# yum install ruby`

やってることは

1. wget で flvstreamerの圧縮されたソースコードをダウンロード
  
2. tar で圧縮ファイルを展開
  
3. 展開したファイルに移動してビルド
  
4. 引数なしで動かしてインストールが正常終了したか動作確認

となります。

動作を確認したら

    $mkdir ~/bin
    $mv flvstreamer ~/bin

とHOMEフォルダ直下にbinを作って、そこに置いておきます。
  
( ~/ はユーザーのHOMEディレクトリ)

それからついでにbashにPATHを通しておきましょう。

`$vi ~/.bashrc`

でBashの設定ファイルを開いてファイルの最後に
  
`PATH="$PATH":~/bin`
  
を追加しておきます。

`$source ~/.bashrc`

として設定を反映させておきましょう。
  
これでどこからでもflvstreamerを呼び出せるようになりました。

### 2. rubyのインストール

次にCaptureStream.rbを動かすためにrubyをインストールします。

以前は yum で入るRubyのバージョンが1.8.5だったので、1.8.7を入れるためにソースからインストールしていたようですが、今は1.8.7が普通に入るので yum でインストールします。

`sudo yum install ruby`

### 3. CaptureStream の設定

まず CaptureStream.rb をダウンロードしてきます。
  
http://sourceforge.jp/projects/capturestream/releases/

ダウンロードしてきた CaptureStream.rbをテキストエディタで開いて設定します。

中に設定方法が書いていますが、

`$default_target = []`

に

`$default_target = ["business1","business2","chinese","french", "italian", "hangeul", "german", "spanish", "russian", "levelup-chinese", "levelup-hangeul"]`

のようにダウンロードしたい講座名を指定します。

これだけで動作は問題ないのですが、
  
自分の場合は保存ファイル名が「毎日ドイツ語\_2012\_06_04」のよりも「毎日ドイツ語-2012-06-04」の方が好きなので

    # 保存ファイル名
    $out_file_hash

の値を「&#8221;%k\_%Y\_%M_%D&#8221; → &#8220;%k-%Y-%M-%D&#8221;」と変更しました。

設定が終わったらnhklangなど適当な名前のフォルダを作ってWinSCPなどでCaptureStream.rbをアップロードします。

ここまでの設定で既に語学講座のダウンロードはできるようになっているはずなので、

    ruby ~/nhklang/CaptureStream.rb

で実際にファイルがダウンロードできてるか確認しておいたほうが良いでしょう。
  
うまくいかなかったらコメント欄に質問をどうぞ。

### 4. cronの設定

あとは毎週決まった時間にダウンロードするためのcronの設定を行います。

    crontab -e

でcronの設定ファイルを開いて

    PATH=/etc:/bin:/sbin:/usr/bin:/usr/sbin:~/bin
    0 11 * * mon ruby ~/nhklang/CaptureStream.rb >> ~/nhklang/Capture.log</pre>
    <p></p>
    
    
    と書いて保存します。これで毎週月曜日の11時にダウンロードが行われます。  
    ただ、実際に来週まで動くかどうか待つのは面倒だという方は時間設定を数分後にして動作確認をすると良いでしょう。
    
    
    ### 参考
    
    
    Ubuntu 10.4 Server上でCaptureStream Ruby版を使ってNHK語学講座をダウンロード: らぶらぶ♪じゃんく  
    <http://app.m-cocolog.jp/t/typecast/27561/29112/69881215?page=2>
    
    
    CaptureStream Ruby版を使ってCentOS 5.5上でNHK語学講座をダウンロードする - fujitaka’s lifelog  
    <http://d.hatena.ne.jp/fujitakastyle/20110403/1301837105>
    
    
    Linuxでの32ビットと64ビットマシンの見分け方。 - IT memorandum  
    <http://d.hatena.ne.jp/jun-ya/20090511/1242028435>
    
    
    CaptureStream Ruby版を使ってCentOS 5.5上でNHK語学講座をダウンロードする - fujitaka’s lifelog  
    <http://d.hatena.ne.jp/fujitakastyle/20110403/1301837105>
    
    
    さくらVPSでRuby on Railsを動かすメモ - @yuumi3のお仕事日記  
    <http://d.hatena.ne.jp/yuum3/20100927/1285567203>
    
    
    [さくらVPS]　デフォルトだと日本語が文字化けするよね？ | DENPA GROOVE  
    <http://jokami.mydns.jp/2010/10/01/%E3%81%95%E3%81%8F%E3%82%89vps%E3%80%80%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E3%81%A0%E3%81%A8%E6%97%A5%E6%9C%AC%E8%AA%9E%E3%81%8C%E6%96%87%E5%AD%97%E5%8C%96%E3%81%91%E3%81%99%E3%82%8B/>
    
    
    cron（クーロン）の設定 - プログラムを定期的に自動実行 [Fedora, RedHat, CentOS] - Linux  
    <http://memorva.jp/memo/linux/cron.php>
    
    
    