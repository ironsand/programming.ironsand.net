---
title: invalid value for BigDecimal が Ruby 2.4から出るようになった
author: 鉄
type: post
date: 2017-12-26T03:32:49+00:00
url: /2017/invalid-value-for-bigdecimal-in-ruby-2-4/
nkweb_code_in_head:
  - default
nkweb_Use_Custom_js:
  - default
nkweb_Use_Custom_Values:
  - default
nkweb_Use_Custom:
  - 'false'
categories:
  - ruby

---
`Ruby 2.3` までは`Bigdecimal`への変換を行う `String#to_d`が数字ではない文字列だった場合に`String#to_i`と同じ`0.0`を返す仕様だったのに`2.4`からは例外を吐くようになったようです。

### Ruby 2.3

<pre class="lang:ruby decode:true " >require 'bigdecimal'
require 'bigdecimal/util'
'abc'.to_d
#=&gt; 0.0</pre>

### Ruby 2.4

<pre class="lang:ruby decode:true " >require 'bigdecimal'
require 'bigdecimal/util'
'abc'.to_d
ArgumentError: invalid value for BigDecimal(): "abc"</pre>

## 対策

バグでした。`gem update bigdecimal` して、`Gemfile`を設定しましょう。
  
<https://github.com/ruby/bigdecimal/issues/51>

<pre class="lang:ruby decode:true " title="Gemfile" >gem 'bigdecimal', '1.3.4'</pre>

<div class='wp_social_bookmarking_light'>
  <div class="wsbl_evernote">
    <a href="#" onclick="Evernote.doClip({ title:'invalid value for BigDecimal が Ruby 2.4から出るようになった', url:'http://programming.ironsand.net/2017/invalid-value-for-bigdecimal-in-ruby-2-4/' });return false;"><img src="http://static.evernote.com/article-clipper.png" /></a>
  </div>
  
  <div class="wsbl_hatena_button">
    <a href="//b.hatena.ne.jp/entry/http://programming.ironsand.net/2017/invalid-value-for-bigdecimal-in-ruby-2-4/" class="hatena-bookmark-button" data-hatena-bookmark-title="invalid value for BigDecimal が Ruby 2.4から出るようになった" data-hatena-bookmark-layout="standard" title="このエントリーをはてなブックマークに追加"> <img src="//b.hatena.ne.jp/images/entry-button/button-only@2x.png" alt="このエントリーをはてなブックマークに追加" width="20" height="20" style="border: none;" /></a>
  </div>
  
  <div class="wsbl_twitter">
    <a href="https://twitter.com/share" class="twitter-share-button" data-url="http://programming.ironsand.net/2017/invalid-value-for-bigdecimal-in-ruby-2-4/" data-text="invalid value for BigDecimal が Ruby 2.4から出るようになった" data-via="ironsand" data-lang="ja">Tweet</a>
  </div>
  
  <div class="wsbl_facebook_like">
    <div id="fb-root">
    </div><fb:like href="http://programming.ironsand.net/2017/invalid-value-for-bigdecimal-in-ruby-2-4/" layout="button_count" action="like" width="100" share="false" show_faces="false" ></fb:like>
  </div>
</div>

<br class='wp_social_bookmarking_light_clear' />