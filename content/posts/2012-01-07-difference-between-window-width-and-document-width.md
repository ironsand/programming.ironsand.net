---
title: $(window).width() と $(document).width() 違い
author: 鉄
type: post
date: 2012-01-07T03:25:58+00:00
url: /2012/difference-between-window-width-and-document-width/
categories:
  - javascript
  - jQuery

---
$(window).width() と $(document).width() や
  
$(window).height() と $(document).height() がどういう時に違う値を返すかわからなかったので検索したら Stack Overflow に簡潔でわかりやすい説明がされてたので紹介します。

> When you have a scrollbar on the webpage.
  
> (スクロールバーが表示されてる時)

わかりやすいですね。一応念のために書いておくと window が「ブラウザの表示領域」で、document が「ページ全体」です。

### 参考

jquery &#8211; When can $(document).width() and $(window).width() show different values? &#8211; Stack Overflow
  
<http://stackoverflow.com/questions/8134741/when-can-document-width-and-window-width-show-different-values>

