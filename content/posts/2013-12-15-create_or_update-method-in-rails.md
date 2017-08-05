---
title: create_or_update 的なメソッドをRailsで使いたいとき
author: 鉄
type: post
date: 2013-12-15T13:50:02+00:00
url: /2013/create_or_update-method-in-rails/
categories:
  - Rails
  - ruby

---
既に該当するモデルの値が存在していたら update で値を更新して、まだ存在しない場合は create で新しくモデルのインスタンスを作成したい時ありませんか？ 少なくとも自分にはありましたし、検索でここに辿り着いたあなたもきっとあると思います。

Railsならきっと簡単な方法があると思ったので調べてみたらありました。

### やり方。

こんな感じでOK。

<pre class="lang:ruby decode:true " >my_class = ClassName.find_or_initialize_by_name(name)

my_class.update_attributes(
   :street_address =&gt; self.street_address,
   :city_name =&gt; self.city_name,
   :federalid =&gt; self.federalid,
   :state_prov_id =&gt; self.state_prov_id,
   :zip_code =&gt; self.zip_code
)</pre>

### 注意点

ちなみに `create_or_update` は `ActiveRecord::Callbacks` の private 関数として用意されてるご様子。

[create\_or\_update (ActiveRecord::Callbacks) &#8211; APIdock][1]

### 参考

[ruby &#8211; create\_or\_update method in rails &#8211; Stack Overflow][2]

