---
title: Net::HTTPを使ってリモートにあるサーバーの最終更新日を取得
author: 鉄
type: post
date: 2017-05-08T07:17:27+00:00
url: /2017/how-to-get-last-modified-from-remote-url-by-using-net-http/
categories:
  - 未分類

---
更新されてる時だけファイルをダウンロードしたいときなどに使う目的で。

```.rb
uri = URI('http://example.com/foo.xls')
Net::HTTP.get_response(uri)['last-modified']
"Mon, 08 May 2017 01:34:46 GMT"
```

<div class='wp_social_bookmarking_light'>
  <div class="wsbl_evernote">
    <a href="#" onclick="Evernote.doClip({ title:'Net::HTTPを使ってリモートにあるサーバーの最終更新日を取得', url:'http://programming.ironsand.net/2017/how-to-get-last-modified-from-remote-url-by-using-net-http/' });return false;"><img src="http://static.evernote.com/article-clipper.png" /></a>
  </div>
  
  <div class="wsbl_hatena_button">
    <a href="//b.hatena.ne.jp/entry/http://programming.ironsand.net/2017/how-to-get-last-modified-from-remote-url-by-using-net-http/" class="hatena-bookmark-button" data-hatena-bookmark-title="Net::HTTPを使ってリモートにあるサーバーの最終更新日を取得" data-hatena-bookmark-layout="standard" title="このエントリーをはてなブックマークに追加"> <img src="//b.hatena.ne.jp/images/entry-button/button-only@2x.png" alt="このエントリーをはてなブックマークに追加" width="20" height="20" style="border: none;" /></a>
  </div>
  
  <div class="wsbl_twitter">
    <a href="https://twitter.com/share" class="twitter-share-button" data-url="http://programming.ironsand.net/2017/how-to-get-last-modified-from-remote-url-by-using-net-http/" data-text="Net::HTTPを使ってリモートにあるサーバーの最終更新日を取得" data-via="ironsand" data-lang="ja">Tweet</a>
  </div>
  
  <div class="wsbl_facebook_like">
    <div id="fb-root">
    </div><fb:like href="http://programming.ironsand.net/2017/how-to-get-last-modified-from-remote-url-by-using-net-http/" layout="button_count" action="like" width="100" share="false" show_faces="false" ></fb:like>
  </div>
</div>

<br class='wp_social_bookmarking_light_clear' />
