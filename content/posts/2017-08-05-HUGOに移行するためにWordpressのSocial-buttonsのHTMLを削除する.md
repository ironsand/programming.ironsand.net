---
title: "HUGOに移行するためにWordpressのSocial ButtonsのHTMLを削除する"
type: post
date: 2017-08-05T16:25:25+09:00
---

WordpressからHUGOに移行する時にTwitterやFacebookなどのソーシャルボタンが本文にハードコーディングされてたので強引に削除しました。
特定の行以降を全て削除するという力技なので間違って想定外のものが消えないか気をつけましょう。

```.rb
# pry
> require 'nokogiri'
Pathname.glob('posts/*.md').each{|f| text = f.read.gsub(/<div class='wp_social_bookmarking_light'>.*/m,''); f.write(text)}
```


