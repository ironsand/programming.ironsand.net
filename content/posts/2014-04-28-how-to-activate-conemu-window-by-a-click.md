---
title: ConEmuのタスクバーのアイコンをクリックしたらすぐにactiveにする
author: 鉄
type: post
date: 2014-04-28T13:11:58+00:00
url: /2014/how-to-activate-conemu-window-by-a-click/
categories:
  - ConEmu
  - 'Shell &amp; Console'
  - Windows

---
デフォルトでは`ConEmu`で複数のタブを開いた状態でタスクバーのアイコンをクリックすると、どのタブを選択するかを選ばないとアクティブにすることができません。

自分はとりあえずクリックしたらアクティブになって欲しいので設定を変えてしまいます。

### 変え方

`ConEmu`のタイトルバーを右クリックして`Settings`を開いて
  
左上の`Find:`のところで`Active console only`と検索します。

すると`Main`->`Task bar`->`Taskbar buttons`の項目の`Show all consoles`がデフォルトで選ばれてると思うので、それを`Active console only (ConEmu window)`に変えて`Save settings`すればOKです。ステキ！

