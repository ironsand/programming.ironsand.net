---
title: WindowsのpostgreSQLをRailsで使うためのセットアップ
author: 鉄
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=442
categories:
  - 未分類

---
WindowsでRailsをpostgreSQLと使うときの初期設定。

### 前提条件

RailsはRailsinstallerでインストール済み
  
Postgresql は Chocolatey で インストール済み

### 設定方法

初期状態だと postgres ユーザーがパスワード `Postgres1234`で登録されてるので、

<pre class="lang:default decode:true " >$ psql -U postgres
ユーザ postgres のパスワード:</pre>

と`psql`コマンドを使ってログイン。`-U`をつけてユーザー名を指定しないと現在のユーザー名になるので注意。

そして自分の場合はユーザー名に`ironsand`を使ってるので

<pre class="lang:default decode:true " >postgres=# create user ironsand with password '';
CREATE ROLE
postgres=# alter user ironsand createdb;
ALTER ROLE</pre>

でユーザーを作成してDB作成権限を付加。

ぱ

