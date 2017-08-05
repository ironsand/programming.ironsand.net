---
title: '[deprecated] I18n.enforce_available_locales とか何とかRailsでエラーが出る時の対処法'
author: 鉄
type: post
date: 2013-12-13T15:50:45+00:00
url: /2013/deprecated-i18n-enforce_available_locales/
categories:
  - Rails
  - ruby

---
Railsでこんなdeprecatedの警告が出てきたので対処方法を調べた。 

<pre class="lang:default decode:true " title="lib/taskの中のファイルを実行した時のエラー" >[deprecated] I18n.enforce_available_locales will default to true in the future. If you really want to skip validation of your locale you can set I18n.enforce_available_locales = false to avoid this message.</pre>

### 対策

<pre class="lang:ruby decode:true " title="config/application.rb" >config.i18n.enforce_available_locales = true</pre>

でOK, \`locale validation\` をきちんとするなら true、どうでも良いならfalseらしい。よくわかんない。

### 参考

[ruby &#8211; Rails I18n validation deprecation warning &#8211; Stack Overflow][1]

