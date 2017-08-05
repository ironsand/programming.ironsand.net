---
title: ffmpeg と sox でドラマから音声を無音部分を除いて抜き出す
author: 鉄
type: post
date: 2014-04-15T16:56:13+00:00
url: /2014/how-to-extract-audios-without-silence-with-ffmpeg-and-sox/
categories:
  - ffmpeg
  - sox

---
英語の勉強にアメリカドラマから音声を抜き出して、その中のサイレンス部分を削除したかったのでやり方を調べたら`ffmpeg`と`sox`で簡単にできることがわかったので、その方法を紹介します。

### 動画から音声を抜き出す

一つの動画から音声を抜き出すときは

    ffmpeg -i input.mp4 -vn output.wav
    

で抜き出せるので

フォルダごとまとめて処理するには

    find . -name '*.mp4' -exec ffmpeg -i '{}' -vn '{}'.wav ';'
    

でフォルダ内の全ての`.mp4`の動画ファイルから`.wav`ファイルが抜き出されます。`-vn`が `no video`のオプションです。

他にも`-acodec copy` として音声ファイルを変換せずに抜き出すこともできます。

### 無音部分を自動検出して削除

次に無音部分を自動的に認識して削除するのに`sox`を使います。やり方によっては`.wav`以外も認識するようにできるようなのですが、うちの環境ではできなかったので`.wav`で処理をしています。

    find . -name '*.wav' -exec sox '{}' '{}'_remove_silence.wav silence 1 0.1 1% -1 0.1 1% ';'
    

で先ほど作った`.wav`ファイルから無音部分が全て削除されました。

### wavをm4aに ffmpeg で変換

`wav`のままだとファイルがでかすぎるので`m4a`に変換します。`mp3`でもいいんですが、`m4a`の方が圧縮効率がいいのでこちらを使います。

    find . -name '*_remove_silence.wav' -exec ffmpeg -i '{}' '{}'.mp3 ';'
    

以上で変換終了です。

### まとめ

この3行を一括変換したいフォルダに`cd`で移動して実行すればOKです。`.wav`ファイルは手動で削除しときましょう。`rm *.wav`でもいいですが。

上記は全て`cygwin`上で行ってますがもちろんLinuxでもMacでも動くはずです。

    find . -name '*.mp4' -exec ffmpeg -i '{}' -vn '{}'.wav ';'
    find . -name '*.wav' -exec sox '{}' '{}'_remove_silence.wav silence 1 0.1 1% -1 0.1 1% ';'
    find . -name '*_remove_silence.wav' -exec ffmpeg -i '{}' '{}'.mp3 ';'
    

### 参考

[ffmpeg &#8211; How to remove silence part from mp3 that is extracted from tv drama &#8211; Unix & Linux Stack Exchange][1]

