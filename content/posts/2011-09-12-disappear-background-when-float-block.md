---
title: floatを指定した要素のみを含むとき背景が表示されない
author: 鉄
type: post
date: 2011-09-12T09:50:10+00:00
url: /2011/disappear-background-when-float-block/
categories:
  - CSS
tags:
  - HTML

---
こんな感じでHTMLを書いたらFirefoxで背景がうまく表示されなかったので調べてみた。<pre class=code><div style="background=#ddd;"> <div style="float:left;">ほげ</div> <div style="float:left;">ほげほげ</div> </div></pre> 

何でそうなるかは下の「参考」のリンク先でわかったのだけれども対策がめんどくさい。なのでこうする事にしました。<pre class=code><div style="background=#ddd;"> <div style="float:left;">ほげ</div> <div style="float:left;">ほげほげ</div> 

<span style="color:red;font-weight:bold;"><div style="clear:both;"></div></span> </div></pre> 

マナーはあんまりよくないですね。書きやすさ優先です。

### 参考

CSSでfloatを指定したボックスを含むボックスの背景が出なくなる件
  
<http://www.fsiki.com/archive/css-doc/float.html>

