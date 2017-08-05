---
title: xyzzy の backward-word と previous-word, forward-word と next-word の違い
author: 鉄
type: post
date: 2011-05-13T16:06:25+00:00
url: /2011/backward-word-previous-word-forward-word-next-word/
categories:
  - xyzzy

---
xyzzy の lisp の関数 backward-word, previous-word, forward-word, next-word の動作の違いがよくわからなかったので、試してみた。 

<span style="background:black;color:white;">黒背景白文字</span>が移動前のカーソルの位置で、<b style="background:#ddd">灰色背景太字</b>が移動後の場所。

<span style=color:blue>backward-word</span>
  
<b style="background:#ddd">1</b>23　<span style="background:black;color:white;">4</span>56　789
  
<b style="background:#ddd">1</b>23<span style="background:black;color:white;">　</span>456　789
  
123　<b style="background:#ddd">4</b><span style="background:black;color:white;">5</span>6　789

<span style=color:blue>previous-word</span>
  
<b style="background:#ddd">1</b>23　<span style="background:black;color:white;">4</span>56　789
  
<b style="background:#ddd">1</b>23<span style="background:black;color:white;">　</span>456　789
  
123　<b style="background:#ddd">4</b><span style="background:black;color:white;">5</span>6　789

<span style=color:blue>forward-word</span>
  
12<span style="background:black;color:white;">3</span><b style="background:#ddd">　</b>456　789
  
123<span style="background:black;color:white;">　</span>456<b style="background:#ddd">　</b>789
  
123　<span style="background:black;color:white;">4</span>56<b style="background:#ddd">　</b>789

<span style=color:blue>next-word</span>
  
12<span style="background:black;color:white;">3</span>　<b style="background:#ddd">4</b>56　789
  
123<span style="background:black;color:white;">　</span><b style="background:#ddd">4</b>56　789
  
123　<span style="background:black;color:white;">4</span>56　<b style="background:#ddd">7</b>89

backward-word と previous-word は同じ動作で forward-word と next-word は動作が異なるらしい。 あってんのかな、これ。

