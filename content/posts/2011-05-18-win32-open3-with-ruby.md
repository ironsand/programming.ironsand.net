---
title: rubyでwin32-open3を使う
author: 鉄
type: post
date: 2011-05-17T20:31:40+00:00
url: /2011/win32-open3-with-ruby/
categories:
  - ruby

---
Rubyで外部のプログラムを起動させて標準エラー出力を得るには open3 を使わないとできないが、 fork() を使ってるためWindowsでは代替の win32-open3 を使って実現する。

まず gem で win32-open3 をインストール

<pre>C:\Users\tetsuya>gem install win32-open3
Successfully installed win32-open3-0.3.2-x86-mswin32-60
1 gem installed
Installing ri documentation for win32-open3-0.3.2-x86-mswin32-60...
Installing RDoc documentation for win32-open3-0.3.2-x86-mswin32-60...</pre>

次にわざとエラを出して標準エラー出力が受け取れるか確認する。

<pre>require 'rubygems'
require 'win32/open3'

stdin, stdout, stderr = *Open3.popen3('ruby -error')
stderr.each{|line|
  print line
}</pre>

その結果

<pre>-e:1: undefined local variable or method `rror' for main:Object (NameError)</pre>

以上。

外部プログラムでエラーでしかほしい情報を返してくれないやつとかいるのでこれが使えると大変便利。

