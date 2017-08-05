---
title: Rails開発してる私が使ってるgemの一覧
author: 鉄
type: post
date: 2013-12-20T02:10:27+00:00
url: /2013/gem-list-for-rails/
categories:
  - Mac
  - Rails
  - ruby

---
Macの環境構築をやり直したので、入れてるgemの一覧を出してみました。

<pre class="lang:default decode:true " title="`gem list`の出力結果" >actionmailer (4.0.0)
actionpack (4.0.0)
activemodel (4.0.0)
activerecord (4.0.0)
activerecord-deprecated_finders (1.0.3)
activesupport (4.0.0)
addressable (2.3.5)
arel (4.0.0)
atomic (1.1.14)
bigdecimal (1.2.0)
buftok (0.2.0)
builder (3.1.4)
bundler (1.3.5)
celluloid (0.15.2)
chunky_png (1.2.8)
coderay (1.1.0)
compass (0.12.2)
compass-normalize (1.4.3)
compass-recipes (0.3.0)
descendants_tracker (0.0.3)
diff-lcs (1.2.5)
equalizer (0.0.8)
erubis (2.7.0)
factory_girl (4.3.0)
factory_girl_rails (4.3.0)
faker (1.2.0)
faraday (0.8.8)
ffi (1.9.3)
formatador (0.2.4)
fssm (0.2.10)
guard (2.2.4)
guard-rspec (4.2.0)
hike (1.2.3)
http (0.5.0)
http_parser.rb (0.5.3)
i18n (0.6.5)
io-console (0.4.2)
json (1.8.1, 1.7.7)
listen (2.2.0)
lumberjack (1.0.4)
mail (2.5.4)
memoizable (0.2.0)
method_source (0.8.2)
mime-types (1.25)
minitest (4.3.2)
multi_json (1.8.0)
multipart-post (1.2.0)
polyglot (0.3.3)
pry (0.9.12.4)
psych (2.0.0)
rack (1.5.2)
rack-test (0.6.2)
rails (4.0.0)
railties (4.0.0)
rake (10.1.0, 0.9.6)
rb-fsevent (0.9.3)
rb-inotify (0.9.2)
rcodetools (0.8.5.0)
rdoc (4.0.0)
rspec (2.14.1)
rspec-core (2.14.7)
rspec-expectations (2.14.4)
rspec-mocks (2.14.4)
rubygems-update (2.1.5)
sass (3.2.12)
simple_oauth (0.2.0)
slop (3.4.7)
spork (0.9.2)
sprockets (2.10.0)
sprockets-rails (2.0.0)
test-unit (2.0.0.0)
thor (0.18.1)
thread_safe (0.1.3)
tilt (1.4.1)
timers (1.1.0)
treetop (1.4.15)
twitter (5.1.1)
tzinfo (0.3.37)</pre>

なので、だいたい名前のわかるやつだけ入れることにします。わかんないのは依存関係のgemか全く使ってないgemなので必要になったらその時に入れることにします。

<pre class="wrap:true lang:default decode:true " >gem install bundler rake compass compass-normalize compass-recipes factory_girl factory_girl_rails faker guard guard-rspec json pry rails rdoc spec spark twitter
</pre>

