---
title: xyzzyをソースからビルドの方法をまとめてみた
author: 鉄
type: post
date: 2011-04-28T21:16:37+00:00
url: /2011/build-xyzzy-from-source/
categories:
  - xyzzy

---
Xyzzy Wiki の [ソースからビルドしてみる3][1] を参考に xyzzy をソースからビルドしてみました。 ファイルを取ってきたり、めんどくさいことが多かったので以下のステップでできるように簡略化。

[xyzzysrc-0.2.2.235-pack][2]
  
これをダウンロードしてあとは01README.txtを見てください。

> 1 Microsoft Visual C++ 2008 Express Edition インストール
  
> 2 env.vbs を叩く (環境変数のセットとafxres.hのコピー)
  
> 3 cd xyzzy/src
  
> 4 nmake (デバッグ版は nmake CFG=d)
  
> 5 ぽけーと待つ
  
> 6 できあがり 

以上です。 何かおかしいところあったら連絡ださい。 俺は何もわかっていませんので。

Unicode Consortium のファイルも同封してますが、ライセンスの確認はとってます。

**2011/05/28追記**

2chで指摘されて気づいたのですが、env.vbs で c:\Program Files\ 配下にファイルの移動を行ってるので UAC が入っているとエラーになります。 UACを一時的に切ってenv.vbs を実行してください。

一度実行してしまえば次回以降ビルドするときにはUAC がオンでも問題ありません。

