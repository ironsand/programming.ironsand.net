---
title: attr_accessible は Rails4では使えなくなりました
author: 鉄
type: post
date: 2013-12-23T09:33:40+00:00
url: /2013/attr_accessible-is-no-more-available-in-rails4/
categories:
  - Rails
  - ruby

---
`attr_accessible`はRails4では使えなくなったのにユーザー管理の定番 gem `devise`ではまだ使っているようなので新しい昨日の Strong parameter に書き換えておきましょう。

### 具体例

devise の設定で User モデルにこんなのが書いてると思うので

<pre class="lang:ruby decode:true " >attr_accessible :email, :password, :password_confirmation</pre>

その行を削除して下の方にこれを追加しましょう。

<pre class="lang:ruby decode:true " title="app/models/user.rb" >private
  def user_params
    params.require(:user).permit(:email, :password, :password_confirmation)
  end</pre>

### 参考

[attr_accessible][1]

