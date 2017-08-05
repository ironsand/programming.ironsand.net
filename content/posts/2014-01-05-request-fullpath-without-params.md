---
title: request.fullpathでparamを使わない
author: 鉄
type: post
date: 2014-01-05T03:24:33+00:00
url: /2014/request-fullpath-without-params/
categories:
  - Rails
  - ruby

---
Railsのrequest.fullpath だと param 以降も受け取ってしまうので、paramの値を使わない時の方法。

### 解決策

splitで邪魔なものをとる方法

<pre class="lang:ruby decode:true " >request.fullpath.split("?")[0]</pre>

`path` を使う方法。こっちのほうがよさそう。

<pre class="lang:ruby decode:true " >request.path</pre>

### 参考

[ruby on rails &#8211; request.fullpath with no parameters &#8211; Stack Overflow][1]

