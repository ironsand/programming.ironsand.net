---
title: Railsで使うpostgresqlのスーパーユーザーを作成する
author: 鉄
type: post
date: 2014-04-25T11:28:56+00:00
url: /2014/create-postgres-superuser-for-rails/
categories:
  - Database
  - Postgresql
  - Rails
  - ruby
  - Windows

---
RailsでPostgresqlを使うときに毎回そのためのユーザーの作成方法を忘れてしまうのでメモ。

### まずユーザーを作成

Windowsで`Chocolatey`を使って`postgresql`をインストールしてると初期パスワードは`Postgres1234`になってるので、

<pre class="lang:sh decode:true " >$ psql.exe -U postgres
ユーザ postgres のパスワード: ←ここでパスワードを入力
psql (9.2.1)
"help" でヘルプを表示します.
postgres=# create user deployer;
CREATE ROLE
postgres=# alter user deployer with superuser;
ALTER ROLE</pre>

これでパスワード無しの`deployer`ユーザーが必要な権限付きで作成される。

※ Linux系のOSなら`sudo -u postgres psql`で`psql`コマンドを使いましょう。

### パスワード無しユーザーでもOKにする

これだけだと`fe_sendauth: no password supplied`というエラーが出てしまうので

`C:\PostgreSQL\data\pg_hba.conf`を開いて

<pre class="lang:default decode:true " ># IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 md5</pre>

を

<pre class="lang:default decode:true " ># IPv4 local connections:
host    all             all             127.0.0.1/32            trust
# IPv6 local connections:
host    all             all             ::1/128                 trust</pre>

に書き換える。

んで管理者権限でコンソールを開いて

net stop postgresql
  
net start postgresql

で`Postgresql`のサービスを再起動させる。
  
残念ながら`restart`は存在しない。なんでや。

### Rails側の設定

あとはいつもどおり`config/database.yml`をこんなかんじに設定します。

<pre class="lang:yaml decode:true " >development:
  &lt;&lt;: *default
  database: project_development
  username: deployer
  password:
  host: localhost
  port: 5432

test:
  &lt;&lt;: *default
  database: project_test
  username: deployer
  password:
  host: localhost
  port: 5432</pre>

んで `$ rake db:create`, `$ rake db:migrate`でデータベースが作成されるのを確認したらOK!

