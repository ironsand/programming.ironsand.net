---
title: link_to で内部にタグがあったりする時はブロックを使いましょう
author: 鉄
type: post
date: 2013-12-11T06:54:04+00:00
url: /2013/link_to-with-block/
categories:
  - Rails
  - ruby

---
Zurb-FoundationとかTwitter bootstrapを使ってると、アイコンをリンク内に含めたくなったりしますよね。こんな感じに

[crayon lang=&#8221;html&#8221;]
  
<i class='general foundicon-refresh'></i> Reload
  
[/crayon]

でもこれをそのまま \`link_to\` で囲んで

[crayon lang=&#8221;html&#8221;]
  
<%= link_to "<i class='general foundicon-refresh'></i> Reload&#8221;,&#8221;http://example.com/reload&#8221; %>
  
[/crayon]

とすると\`<i>\`タグがHTMLエスケープされて悲しい事態になるんです。

### 対策

なのでそういう時は \`link_to\` さんはブロックが取れるのでブロックを使って処理しましょう。ブロックの返り値がリンクのテキストになります。

[crayon lang=&#8221;html&#8221;]
  
<%= link_to "http://example.com/reload", class: 'reload' do %>
    
<i class='general foundicon-refresh'></i> Reload
  
<% end %>
  
[/crayon]

ちなみに \`button_to\` も同じような関数なのでこういう風にかけます。

[crayon lang=&#8221;html&#8221;]
  
<%= button_to "", class: 'small radius' do %>
    
<i class='general foundicon-refresh'></i> Reload
  
<% end %>
  
[/crayon]

これ知らない時に必死にHTMLエスケープされないために何をすればよいのかを探しまくったのは今では良い思い出でもなんでもありません。時間返せ。

### 参考

[ruby on rails &#8211; link_to in helper with block &#8211; Stack Overflow][1]

