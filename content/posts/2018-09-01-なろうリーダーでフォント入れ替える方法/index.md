---
title: なろうリーダーでフォント入れ替える方法
author: 鉄
type: post
date: 2018-09-01T08:09:53+00:00
url: /2018/なろうリーダーでフォント入れ替える方法/
categories:
  - Android

---
### こんな感じになります

<img alt="なろうリーダーサンプル" src="narou-font.png" width=240/>

### 設定方法など

なろうリーダーで縦書きができるようになったのですが、Kindleなどど違ってIPAフォントをアプリの機能でダウンロードしてインストールすることはできないようです。

`設定`の`キャッシュ設定`→`保存先`に

    /storage/emulated/0/Android/data/com.tscsoft.naroureader/files
    

のようにキャッシュ用のフォルダが示されてるので、以下のサイトからフォントを落としてきてこのフォルダにコピーすれば設定からIPAフォントが選べるようになります。

<https://ipafont.ipa.go.jp/old/ipafont/download.html>

ファイルの移動には`Airmore`を使うと便利です。

`Airmore`で転送する際には頭の`/storage/emulated/0/`を無視して`Android`ディレクトリから選んでいけばOKです。`files/fonts`となっていますのでその中に入れましょう。  
