---
title: ActiveSupport::Inflectorで定義した頭字語が`has_many`を解釈してくれない時の解決法
author: 鉄
type: post
date: 2015-02-02T07:23:20+00:00
url: /2015/activesupportinflectorで定義した頭字語がhas_manyを解釈してくれない/
categories:
  - Rails
  - ruby

---
Rubyの命名規則としてクラス名は通常は`CamelCase`で記述しますが、`HTTP`などの頭字語(Acronym)はそのまますべて大文字で記述します。

Railsで頭字語のクラス名を使うときはモデル等を生成する前に設定で以下の記述を行っておくと自動的に認識してくれます。

<pre class="lang:ruby decode:true " title="config/initializers/inflections.rb" >ActiveSupport::Inflector.inflections(:en) do |inflect|
    inflect.acronym 'GNU'
end
</pre>

ただ`has_many`でこのクラスを持とうとすると以下のエラーになってしまいます。

> LoadError: Unable to autoload constant Gnu, expected
    
> /Users/ironsand/dev/myproject/app/models/gnu.rb to define it

### 対策

クラス名を明示的に指定するとOKです。

<pre>has_many :gnus, class_name => "GNU"</pre>

