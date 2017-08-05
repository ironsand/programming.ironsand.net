---
title: FormのSubmitでZurb-FoundationのReveal Modalを使う方法
author: 鉄
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=295
categories:
  - 未分類

---
Zurb-FoundationのmodalダイアログをFormのSubmitをイベントにして呼び出すと、Submitイベントが食われてしまうことがわからずにしばらくハマる。ふぁっく。

### 対処法

submitのイベントをjavascriptで検知しといてそこからModalダイアログを出すように引っ掛けるとOK。

### 参考

[Opening Reveal Model With Form Submit Button &#8211; Google Groups][1]

