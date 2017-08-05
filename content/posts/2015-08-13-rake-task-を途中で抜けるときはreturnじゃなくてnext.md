---
title: rake task を途中で抜けるときはreturnじゃなくてnext
author: 鉄
type: post
date: 2015-08-13T07:37:22+00:00
url: /2015/rake-task-を途中で抜けるときはreturnじゃなくてnext/
categories:
  - Rails
  - ruby

---
<pre class="lang:ruby decode:true " >task :do_something do
  return if some_condition?
  do_job
end
</pre>

というように条件に合致しない時に `return`を使って処理を抜けようとするとこんなエラーになります。

<pre class="lang:default decode:true " >LocalJumpError: unexpected return</pre>

これは rake task がメソッドではなくブロックだから起きるので `next` を使ってやりましょう。それで抜けれます。

<pre class="lang:ruby decode:true " >task :do_something do
  next if some_condition?
  do_job
end
</pre>

ちなみに`next`は気持ち悪いんのでせめて`break`を使いたいと思ったんですが、それだと

<pre class="lang:default decode:true " >LocalJumpError: break from proc-closure
</pre>

になってしまいます。

### 参考

[ruby &#8211; How do I return early from a rake task? &#8211; Stack Overflow][1]

