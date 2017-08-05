---
title: cygwinで.bash_profileが読み込まれなかった時の対処法
author: 鉄
type: post
date: 2012-11-10T02:33:37+00:00
url: /2012/how-to-load-bash_profile-by-cygwin/
categories:
  - cygwin

---
cygwinでちゃんとHOMEの環境変数を設定してるのに ~/.bash_profileが読み込まれなかったのでその時の対処法。

### 問題点

結局問題だったのはbashを立ち上げた時に出てくるこのエラーメッセージを無視してたのが原因でした。

> Your group is currently &#8220;mkpasswd&#8221;.
> 
> This indicates that your gid is not in /etc/group and your uid is not in /etc/passwd.
> 
> The /etc/passwd (and possibly /etc/group) files should be rebuilt. See the man pages for mkpasswd and mkgroup then, for example, run
> 
> mkpasswd -l [-d] > /etc/passwd
  
> mkgroup -l [-d] > /etc/group
> 
> Note that the -d switch is necessary for domain users.

/etc/passwd を確認してみると、確かに今使ってるWindowsでのユーザ名が表示されていない。いつもcygwinのフォルダは上書きし続けて使ってるのでインストール時に既に /etc/passwd があった場合に自動更新されないみたいですね。

指示通りに
  
`mkpasswd -l > /etc/passwd<br />
mkgroup -l > /etc/group`
  
すると.bash_profileを読み込むようになりました。

### HOMEの設定方法

ちなみにHOMEの設定方法は

> HOME from the Windows environment, translated to POSIX form.
> 
> The entry in /etc/passwd
> 
> /home/USERNAME
> 
> When using Cygwin from the network (telnet, ssh,&#8230;), HOME is set from /etc/passwd.

[cygwin FAQ][1]
  
にあるように

1. Windowsの環境変数HOME
  
2. /etc/passwd にある記述
  
3. /home/USERNAME
  
4. ただし telnet,sshとかのネットワーク経由の場合は /etc/passwd が優先される

とのことです。

このときcygdrive外のフォルダを指定するには Windowsの環境変数に /cygdrive/c/ などから始まる記述を行います。

自分の場合はDropboxの直下にhomeフォルダを作り、それを複数環境で共有してるので
  
/cygdrive/p/dropbox/home とHOMEに設定しています。

### 参考

Dropbox » Webserviceを使っていこう
  
<http://webservice.ironsand.net/category/dropbox/>

