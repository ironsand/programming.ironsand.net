---
title: Net::HTTPを使ってリモートにあるサーバーの最終更新日を取得
author: 鉄
type: post
date: 2017-05-08T07:17:27+00:00
url: /2017/how-to-get-last-modified-from-remote-url-by-using-net-http/
categories:
  - 未分類

---
更新されてる時だけファイルをダウンロードしたいときなどに使う目的で。

```.rb
uri = URI('http://example.com/foo.xls')
Net::HTTP.get_response(uri)['last-modified']
"Mon, 08 May 2017 01:34:46 GMT"
```
