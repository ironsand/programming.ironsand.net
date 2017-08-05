---
title: Raspberry Pi に Avahi を入れてSSH接続を簡単に
author: 鉄
type: post
date: 2015-02-16T12:30:39+00:00
url: /2015/raspberry-pi-に-avahi-を入れてssh接続を簡単に/
categories:
  - Raspberry Pie

---
[初めてのラズベリーパイ 【購入からSSH接続まで】][1] で SSH を使ってラズベリーパイに接続ができたのですが、DHCPでローカルのIPアドレスを振り分けてる時は振り当てられてるIPアドレスを調べるためだけにラズパイにキーボードとディスプレイをさして作業する必要がでてくるので非常にめんどくさいことになります。

### Avahi

そこで`Avahi`というソフトを使えば `hosts` ファイルがなくてもローカルネットワーク内の他のPCからIPアドレスではなく名前で参照できるようになります。。Macの`共有`機能などで使われている `Bonjour` と同等のものなんだとか。

### インストール

`/etc/hostname` に保存されてる名前で接続できるようになるので初期設定の`raspberrypi`という名前を別のものに変更しておきましょう。

    sudo vi /etc/hostname
    

Avihaのインストールはいつもどおり`apt-get`でインストールできます。

    sudo apt-get -y install avahi-daemon 
    

### スタートアップに登録

このままでは起動時に自動的に`Avahi`が立ち上がってくれませんので

<pre class="lang:sh decode:true " >sudo update-rc.d avahi-daemon defaults</pre>

でスタートアップにも登録しておきましょう。

### ※ 追記

次回使おうとしたら動かなくなってしまってました。 `/etc/hosts`を編集しないといけなかったようです。

    127.0.0.1       localhost
    ::1             localhost ip6-localhost ip6-loopback
    fe00::0         ip6-localnet
    ff00::0         ip6-mcastprefix
    ff02::1         ip6-allnodes
    ff02::2         ip6-allrouters
    
    127.0.1.1       raspberrypi
    

となっていますので`raspberrypi`の部分を変更した名前に変えておきます。

### 使い方

インストールが終わったらクライアントから`ssh pi@raspberry.local`のような形で `pi@自分で決めた名前.local`で接続できるようになります。

それではみなさん楽しい Raspberry Pie 生活をお過ごしください。 ノシ

### 参考

[RaspberryPi &#8211; Raspberry Pi を無線 LAN 経由で SSH 接続できるようにする &#8211; Qiita][2]

