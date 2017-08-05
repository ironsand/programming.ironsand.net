---
title: `/var/www/`以下のパーミッションまとめ
author: 鉄
type: post
date: 2014-04-10T03:52:23+00:00
url: /2014/permission-about-var-www/
categories:
  - PHP
  - VPS
  - Wordpress

---
`/var/www`配下のパーミッションをどうすべきかについて情報が錯綜してて困ったので自分なりに調べたことをまとめておきます。

サーバープロセスが直接ファイルの変更を行うか、複数人管理かがどうかで結構変わるのでめんどくさくなってるみたいですね。

### まとめ

  1. サーバープロセスがファイルの変更を行わず、sudo可ユーザーのみが変更
  
    `/var/www` 以下は全て `root:root`
  
    理由：apache, nginx などのプロセスが乗っ取られてもroot権限がないと改変できないため

  2. サーバープロセスがファイルの変更を行わず、sudo不可のユーザーも変更
  
    `/var/www/site` を `ftp-user:root` に。
  
    複数ユーザーがFTPでアクセスして書き込み権を持つなら `ftp-user:ftp-user`で適当にユーザーをグループに追加

  3. サーバープロセスがファイルの変更を行う(WordPressなど)、
  
    `/var/www/site` 以下の必要なフォルダ、ファイル_だけ_を `ftp-user:www-user` にして
  
    サーバープロセスのユーザーをwww-userに追加、apache所有には_絶対にしない_。

