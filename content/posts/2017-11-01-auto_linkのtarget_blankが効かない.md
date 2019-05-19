---
title: 'simple_formatを適用させるとauto_linkの target: ‘_blank’が効かない'
author: 鉄
type: post
date: 2017-11-01T14:07:45+00:00
url: /2017/auto_linkのtarget_blankが効かない/
nkweb_code_in_head:
  - default
nkweb_Use_Custom_js:
  - default
nkweb_Use_Custom_Values:
  - default
nkweb_Use_Custom:
  - 'false'
categories:
  - Rails
  - ruby

---
### 状態

こういうふうに書いたら`target: '_blank'`が効かなくて困った。

    simple_format(auto_link(text, :target => "_blank" ))
    

### 対策

`simple_format`は`a`タグの`target`属性を取り除いてしまうので順番を入れ替えて、こう書くとOK。

    auto_link(simple_format(text), :target => "_blank" )
    

### 参考

https://github.com/tenderlove/rails_autolink/issues/20#issuecomment-24818734

<div class='wp_social_bookmarking_light'>
  <div class="wsbl_evernote">
    <a href="#" onclick="Evernote.doClip({ title:'simple_formatを適用させるとauto_linkの target: &#8216;_blank&#8217;が効かない', url:'http://programming.ironsand.net/2017/auto_link%e3%81%aetarget_blank%e3%81%8c%e5%8a%b9%e3%81%8b%e3%81%aa%e3%81%84/' });return false;"><img src="http://static.evernote.com/article-clipper.png" /></a>
  </div>
  
  <div class="wsbl_hatena_button">
    <a href="//b.hatena.ne.jp/entry/http://programming.ironsand.net/2017/auto_link%e3%81%aetarget_blank%e3%81%8c%e5%8a%b9%e3%81%8b%e3%81%aa%e3%81%84/" class="hatena-bookmark-button" data-hatena-bookmark-title="simple_formatを適用させるとauto_linkの target: &#8216;_blank&#8217;が効かない" data-hatena-bookmark-layout="standard" title="このエントリーをはてなブックマークに追加"> <img src="//b.hatena.ne.jp/images/entry-button/button-only@2x.png" alt="このエントリーをはてなブックマークに追加" width="20" height="20" style="border: none;" /></a>
  </div>
  
  <div class="wsbl_twitter">
    <a href="https://twitter.com/share" class="twitter-share-button" data-url="http://programming.ironsand.net/2017/auto_link%e3%81%aetarget_blank%e3%81%8c%e5%8a%b9%e3%81%8b%e3%81%aa%e3%81%84/" data-text="simple_formatを適用させるとauto_linkの target: &#8216;_blank&#8217;が効かない" data-via="ironsand" data-lang="ja">Tweet</a>
  </div>
  
  <div class="wsbl_facebook_like">
    <div id="fb-root">
    </div><fb:like href="http://programming.ironsand.net/2017/auto_link%e3%81%aetarget_blank%e3%81%8c%e5%8a%b9%e3%81%8b%e3%81%aa%e3%81%84/" layout="button_count" action="like" width="100" share="false" show_faces="false" ></fb:like>
  </div>
</div>

<br class='wp_social_bookmarking_light_clear' />