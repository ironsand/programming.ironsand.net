---
title: linuxで特定のファイルの最終行だけ削除する
author: 鉄
type: post
date: 2014-03-27T11:57:07+00:00
url: /2014/delete-list-line-of-a-file-in-linux-by-using-sed/
categories:
  - Commands
  - DigitalOcean
  - sed
  - ssh
  - VPS

---
Digital OceanではOSを気軽にDropletで作成して、気軽にポイポイ捨てれるのが売りですが、そのせいで `ssh`で新しく繋ぎ直したホストに繋ごうとすると

<pre class="lang:default decode:true " >@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
Please contact your system administrator.
Add correct host key in /home/ironsand/.ssh/known_hosts to get rid of this message.
Offending RSA key in /home/ironsand/.ssh/known_hosts:18
RSA host key for 107.170.114.105 has changed and you have requested strict checking.
Host key verification failed.</pre>

と怒られてしまう。

毎回、手動で該当行を削除するのはめんどくさいので最終行を削除するコマンドを使うことにした。

### やり方

<pre class="lang:sh decode:true " >sed -ie '$d' ~/.ssh/known_hosts</pre>

でOK。ブラボー、ブラボー！

ちなみに&#8221;linuxで&#8221;とは書きましたが、自分はWindowsのcygwinで使ってます。

### 参考

[linux &#8211; Deleting last line of a file &#8211; Stack Overflow][1]

