---
title: irb上でrubyスクリプトの実行速度を測る
author: 鉄
type: post
date: 2014-04-26T16:59:23+00:00
url: /2014/benchmark-ruby-script-in-irb/
categories:
  - ruby
  - time

---
例えば `foo.rb`というRubyスクリプトの実行時間をシェル上で知りたかったら`time foo.rb`とすればいいわけですが、残念ながら`irb`上では`time`コマンドをそのまま使うことができません。

### 解決策

標準で用意されている`Benchmark`ライブラリを使えばOK.

<pre class="lang:ruby decode:true " >irb(main)&gt; require 'benchmark'
irb(main)&gt; puts Benchmark.measure { "a"*1_000_000_000 }
0.350000   0.400000   0.750000 (  0.835234)</pre>

こんな感じで表示されます。

`0.750000`がCPUを使った時間で`0.835234`が実際にかかった時間。
  
気にしないといけないのはCPUを実際に使ってたじかんなので前者のほうになります。

ちなみに自分の環境だと裏で動画のエンコードを走らせながらVirtualBox上のOSでやってたのでCPU使用時間の50倍ぐらい実際にかかってしまってました。

### 参考

[Module: Benchmark (Ruby 2.1.1)][1]

[When benchmarking, what causes a lag between CPU time and "elapsed real time"? &#8211; Stack Overflow][2]

