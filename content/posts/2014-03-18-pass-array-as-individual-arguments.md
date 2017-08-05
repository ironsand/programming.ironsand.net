---
title: 複数の引数を取る関数に配列で値を渡す
author: 鉄
type: post
date: 2014-03-17T17:54:36+00:00
url: /2014/pass-array-as-individual-arguments/
categories:
  - ruby

---
rubyで `def foo(arg1, arg2, arg3)` な関数があった時に `values = [1, 2, 3]` という値を渡そうとして

`foo values` とすると `TypeError: no implicit conversion of Array into Integer` というエラーになります。

### 解決策

この配列をいうなれば”展開”して渡したいわけですが、やり方がわからなかったので調べました。

`foo *values` のようにまるでC言語みたいな渡し方をすればOK.

### 参考

[caiustheory.com/sending-array-elements-as-individual-arguments-in-ruby][1]

