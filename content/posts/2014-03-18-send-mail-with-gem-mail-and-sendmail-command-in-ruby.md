---
title: gem `mail` と sendmail を使って簡単にRubyでメール送信
author: 鉄
type: post
date: 2014-03-18T12:29:20+00:00
url: /2014/send-mail-with-gem-mail-and-sendmail-command-in-ruby/
categories:
  - ruby

---
`net/smtp` ライブラリを使うよりも `gem mail` を使えば簡単にメールが送れるらしいので調べてみた。

### 方法

まず `mail` gem が必要なので `$ gem install mail` でインストールする。

んで、下のように書けばOK!

<pre class="lang:ruby decode:true " >require 'mail'
mail = Mail.new do
  from     'me@ironsand.net'
  to       'recipient@exmaple.com'
  subject  'Here is the image you wanted'
  body     'Body'
end

mail.delivery_method :sendmail

mail.deliver</pre>

### 注意点

Macでは動かなかったので、VPS上の`CentOS 6.4`で試してます。
  
25版ポートを開けるのを忘れずに。

### 参考

[email &#8211; Ruby Mail gem: Connection refused &#8211; connect(2) (Errno::ECONNREFUSED) &#8211; Stack Overflow][1]

