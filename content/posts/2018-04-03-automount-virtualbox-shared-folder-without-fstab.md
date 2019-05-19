---
title: VirtualBoxの共有フォルダを起動時に自動マウント(fstabは使わない)
author: 鉄
type: post
date: 2018-04-02T23:37:46+00:00
url: /2018/automount-virtualbox-shared-folder-without-fstab/
categories:
  - Virtualbox

---
Virtualboxの共有フォルダ機能は便利なんですが、`/etc/fstab`に追加しようとすると`vboxsf`がマウント時にまだ読み込まれてないとかでディストリビューションによっては使えません。

あまり行儀はよくないのですが`/etc/rc.local`でマウントしてしまえば解決です。

<pre class="lang:sh decode:true " title="/etc/rc.local" >mount -t vboxsf share /home/ironsand/share || /bin/true
exit 0
</pre>

`exit 0`より前に書くことだけ気をつけましょう。

### 参考

[How to mount a VirtualBox shared folder at startup?][1]

 [1]: https://askubuntu.com/a/578585/188942