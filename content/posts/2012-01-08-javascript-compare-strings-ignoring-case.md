---
title: javascript で大文字、小文字を無視して文字列比較
author: 鉄
type: post
date: 2012-01-07T21:12:25+00:00
url: /2012/javascript-compare-strings-ignoring-case/
categories:
  - javascript

---
javascript で大文字、小文字を区別しないで文字列比較がしたい時は、そういう演算子は用意されてないので toLowerCase() で全部小文字にして比較しちゃいましょう。

こんな感じ。

<pre>function check(){
  foo="ABC";
  bar="abc";
  if(foo.toLowerCase() == bar.toLowerCase()){ //大文字小文字を無視
    alert("ok!!");
  }else{
    alert("NG!");
  }
}</pre>

ちなみに英語で「大文字、小文字を区別しない。」と言いたい時は case-insensitive を使えばよいそうですよ。

