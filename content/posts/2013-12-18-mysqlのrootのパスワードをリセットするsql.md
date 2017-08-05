---
title: MySQLのrootのパスワードをリセットするSQL
author: 鉄
type: post
date: 2013-12-17T16:22:13+00:00
url: /2013/mysqlのrootのパスワードをリセットするsql/
categories:
  - MySQL

---
MySQLのパスワードがわからなくなった時に使う root のパスワードリセットのためのSQL文

<pre class="lang:mysql decode:true " >UPDATE mysql.user SET Password=PASSWORD('masterpassword') WHERE User='root';
FLUSH PRIVILEGES;
</pre>

