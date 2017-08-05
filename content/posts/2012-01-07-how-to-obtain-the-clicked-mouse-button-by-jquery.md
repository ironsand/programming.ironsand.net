---
title: jQueryでマウスの右クリック、左クリックを判断する
author: 鉄
type: post
date: 2012-01-07T03:41:05+00:00
url: /2012/how-to-obtain-the-clicked-mouse-button-by-jquery/
categories:
  - javascript
  - jQuery

---
jQuery を使って

「クリックされた時に左なら要素を消して、右なら何もしない。」

という動作をさせようと思ったら日本語だと検索してもすぐに答えが出てこなかったので、また stackoverflow から解説を紹介します。

実際のコードがこちら。

<pre>$('#element').mousedown(function(event) {
    switch (event.which) {
        case 1:
            alert('Left mouse button pressed');
            break;
        case 2:
            alert('Middle mouse button pressed');
            break;
        case 3:
            alert('Right mouse button pressed');
            break;
        default:
            alert('You have a strange mouse');
    }
});
</pre>

mousedown の時に渡されるイベントを確認して場合わけすればよい、と。

つまり左クリックで要素を隠すにはこうします。

<pre>//左クリックされると foo を隠す
$(".foo").click(function(e){
  if(e.which == 1){ //左クリック
    $(this).hide("fast");
  }
});</pre>

### 他の方法

頻繁に使うのであれば jquery.detailclick.js を入れてこんな風に使えるようにしておくとよいかもしれません。やっぱりこちらの方が jQuery っぽくて見やすいですね。

<pre>$("target").rightClick(function()<br />
  {<br />
    $(this).text('右クリックされました！').css('background-color', '#ff3399');<br />
});</p>


<pre>


<h3>
  参考
</h3>


<p>
  javascript - How to distinguish between left and right mouse click with jQuery? - Stack Overflow<br />
  <a href="http://stackoverflow.com/questions/1206203/how-to-distinguish-between-left-and-right-mouse-click-with-jquery">http://stackoverflow.com/questions/1206203/how-to-distinguish-between-left-and-right-mouse-click-with-jquery</a><br />
  JSNote - 左、中、右クリックのカスタムイベントを追加するjQueryプラグイン<br />
  <a href="http://jsnt.blog.fc2.com/blog-entry-3.html">http://jsnt.blog.fc2.com/blog-entry-3.html</a>
</p>


