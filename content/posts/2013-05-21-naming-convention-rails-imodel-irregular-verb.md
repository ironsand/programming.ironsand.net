---
title: RailsでModelが不規則名詞だった場合のControllerの命名規則
author: 鉄
type: post
date: 2013-05-21T07:35:49+00:00
url: /2013/naming-convention-rails-imodel-irregular-verb/
categories:
  - Rails
  - ruby

---
RailsのModelは常に単数名詞、そしてControllerはその名詞の複数形という規則がありますが、Modelが”Child&#8221;などの不規則変化名詞だった時にController名は**Childrenなのか、Childsなのかがわからなかった**ので調べました。

### 答え

プログラム的には当然簡単に処理できるChildsだと思ったけども実際はちゃんと不規則変化にも対応してるらしくChildrenが正解です。

### その他の不規則名詞

他の不規則名詞は
  
<https://github.com/rails/rails/blob/4-0-0/activesupport/lib/active_support/inflections.rb>

に載っているんですが、

<pre class="wrap:true lang:default decode:true " >inflect.irregular('person', 'people')
    inflect.irregular('man', 'men')
    inflect.irregular('child', 'children')
    inflect.irregular('sex', 'sexes')
    inflect.irregular('move', 'moves')
    inflect.irregular('cow', 'kine')
    inflect.irregular('zombie', 'zombies')
</pre>

zombieって不規則名詞なの…？

cow→kineの変化はそもそも英単語がわかりませんでした、、

### Zombieが不規則名詞の理由 ([2013/12/14] 追記)

単数形から複数形への変化は規則通りですが、複数形から単数形への変化 zombies -> zombie が不規則で、規則通り変化させてしまうと zombies -> zomby になってしまうから不規則名詞らしいです。英語は難しいですね。

### 情報元

[Model and Controller&apos;s naming rule for irregular noun in Rails &#8211; Stack Overflow][1]

