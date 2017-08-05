---
title: OmniauthとDeviseの設定ファイルを両方同時に使うとルーティングがおかしくなる
author: 鉄
type: post
date: 2013-12-23T09:28:29+00:00
url: /2013/must-not-use-omniauthdevise-config-file-sametime/
categories:
  - Rails
  - ruby

---
何故だか理由はさっぱりわかりませんが、どうにもおかしな動きが `route.rb` をいくらいじってもなおらないので色々情報を探してたら、config の `omniauth.rb` を消したら動きました。

consumer_key とかは devise.rb に書いておきましょう。

### 参考

[ruby on rails 3 &#8211; Authentication failure : Devise + OmniAuth + Twitter &#8211; Stack Overflow][1]

