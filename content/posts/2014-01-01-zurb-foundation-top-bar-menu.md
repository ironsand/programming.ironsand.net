---
title: Zurb Foundation のトップバーの右上のメニューを消えないようにする
author: 鉄
type: post
date: 2014-01-01T14:05:29+00:00
url: /2014/zurb-foundation-top-bar-menu/
categories:
  - CSS
  - Rails
  - ruby
  - Sass
tags:
  - Foundation

---
Zurb Foundationのトップバーの右上のメニューですが、デフォルトでは幅が940pxを切るとMenuに折りたたまれてしまうという結構広い設定になっています。

もうちょっと幅が狭くても出るようにしたかったので修正しました。

### 対策

設定ファイルを以下のように書き換えます。環境はRailsです。

<pre class="lang:sass decode:true " title="app/assets/stylesheets/foundation_and_overrides.scss" >// $topbar-breakpoint: 940 !default; // Change to 9999px for always mobile layout
$topbar-breakpoint: emCalc(600px); </pre>

ちなみに[Menu]自体がでなくて少し困ったのですが`toggle-topbar menu-icon` を設定してなかったのが原因だったようです。

<pre class="lang:xhtml decode:true " title="app/views/layouts/_header.html.erb" >&lt;ul class="title-area"&gt;
      &lt;li class="name"&gt;
    &lt;h1&gt;&lt;%= link_to "Site Title", root_path %&gt;&lt;/a&gt;&lt;/h1&gt;
      &lt;/li&gt;
      &lt;li class="toggle-topbar menu-icon"&gt;&lt;a href="#"&gt;&lt;span&gt;Menu&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;</pre>

