---
title: zshでhistoryに実行時間も残す方法
author: 鉄
type: post
date: 2017-10-18T22:47:37+00:00
url: /2017/zshでhistoryに実行時間も残す方法/
nkweb_code_in_head:
  - default
nkweb_Use_Custom_js:
  - default
nkweb_Use_Custom_Values:
  - default
nkweb_Use_Custom:
  - 'false'
categories:
  - 未分類

---
`bash`だと`HISTTIMEFORMAT="[%F %T] "`とか`~/.bashrc`に書いておけばログに実行した日時も残しておけるんだけど`zsh`だと`HISTTIMEFORMAT`がないらしいので方法を調べてみた。

### 設定しなくてOK

デフォルトで使えるようになってるらしい

<pre><code class="sh">$ history -E
    1   2.12.2013 14:19  history -E

$ history -i
    1  2013-12-02 14:19  history -E

$ history -D
    1  0:00  history -E
    2  0:00  history -i
</code></pre>

だけでOK。

### 参考

<https://unix.stackexchange.com/questions/103398/datetime-stamp-when-running-history-command-in-zsh-shell>

<div class='wp_social_bookmarking_light'>
  <div class="wsbl_evernote">
    <a href="#" onclick="Evernote.doClip({ title:'zshでhistoryに実行時間も残す方法', url:'http://programming.ironsand.net/2017/zsh%e3%81%a7history%e3%81%ab%e5%ae%9f%e8%a1%8c%e6%99%82%e9%96%93%e3%82%82%e6%ae%8b%e3%81%99%e6%96%b9%e6%b3%95/' });return false;"><img src="http://static.evernote.com/article-clipper.png" /></a>
  </div>
  
  <div class="wsbl_hatena_button">
    <a href="//b.hatena.ne.jp/entry/http://programming.ironsand.net/2017/zsh%e3%81%a7history%e3%81%ab%e5%ae%9f%e8%a1%8c%e6%99%82%e9%96%93%e3%82%82%e6%ae%8b%e3%81%99%e6%96%b9%e6%b3%95/" class="hatena-bookmark-button" data-hatena-bookmark-title="zshでhistoryに実行時間も残す方法" data-hatena-bookmark-layout="standard" title="このエントリーをはてなブックマークに追加"> <img src="//b.hatena.ne.jp/images/entry-button/button-only@2x.png" alt="このエントリーをはてなブックマークに追加" width="20" height="20" style="border: none;" /></a>
  </div>
  
  <div class="wsbl_twitter">
    <a href="https://twitter.com/share" class="twitter-share-button" data-url="http://programming.ironsand.net/2017/zsh%e3%81%a7history%e3%81%ab%e5%ae%9f%e8%a1%8c%e6%99%82%e9%96%93%e3%82%82%e6%ae%8b%e3%81%99%e6%96%b9%e6%b3%95/" data-text="zshでhistoryに実行時間も残す方法" data-via="ironsand" data-lang="ja">Tweet</a>
  </div>
  
  <div class="wsbl_facebook_like">
    <div id="fb-root">
    </div><fb:like href="http://programming.ironsand.net/2017/zsh%e3%81%a7history%e3%81%ab%e5%ae%9f%e8%a1%8c%e6%99%82%e9%96%93%e3%82%82%e6%ae%8b%e3%81%99%e6%96%b9%e6%b3%95/" layout="button_count" action="like" width="100" share="false" show_faces="false" ></fb:like>
  </div>
</div>

<br class='wp_social_bookmarking_light_clear' />