---
title: PythonのGUI,Tkinterのエラー対処
author: 鉄
type: post
date: 2011-02-26T06:38:20+00:00
url: /2011/tkinter-importerror/
categories:
  - python

---
PythonのGUI,Tkinterを使おうとこのページの一番上のサンプルを動かそうとすると動かず第一歩をくじかれる。
  
<http://www.pythonware.com/library/tkinter/introduction/hello-tkinter.htm>

エラーメッセージはこんなの。
  
`ImportError: No module named Tkinter`

環境はWindows7でPython3.0.1 Portable。

エラーメッセージで検索しても「yumを使ってモジュールインストールしろ。」とかLinux向けの情報しか出てこない。 適当にあさってやっと見つけた解決策はこれ。

`from Tkinter import *`
  
を
  
`from tkinter import *`
  
に変える。 どうも Python3からmodule名の大文字小文字が変更されたのが原因だったようだ。
  

  


