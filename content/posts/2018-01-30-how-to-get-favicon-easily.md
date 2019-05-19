---
title: Faviconを取得する簡単な方法
author: 鉄
type: post
date: 2018-01-29T20:00:47+00:00
url: /2018/how-to-get-favicon-easily/
categories:
  - ruby

---
faviconを取得したければ`<link rel="icon" href="favicon.ico">`を探すなどの正攻法がありますが、
  
色々と例外があるようなのでめんどくさい時はGoogleさんに任せてしまいましょう。

    URI('https://www.google.com/s2/favicons?domain_url=stackoverflow.com').read
    

でとれます。

### 参考

https://stackoverflow.com/questions/5119041/how-can-i-get-a-web-sites-favicon
