---
title: 返り値が false か 整数の関数で `0` をtrueと判定する方法
author: 鉄
type: post
date: 2013-12-10T14:03:47+00:00
url: /2013/recognize-0-as-a-true-in-php/
categories:
  - PHP

---
WordPressの `has_filter()`は返り値が int|boolean なので普通に `if(has_filter())` で処理しちゃうと `` が返ってきた時に意図しない結果になってしまいます。

### 解決策

なのでそういう時は `if(is_int(has_filter()))` を使いましょう。

### 参考

[wordpress &#8211; recognize `` as a true in PHP if statement &#8211; Stack Overflow][1]

