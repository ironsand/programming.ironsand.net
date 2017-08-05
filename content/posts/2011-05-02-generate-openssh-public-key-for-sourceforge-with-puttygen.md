---
title: SourceForgeに公開鍵をputtygen.exeで生成する
author: 鉄
type: post
date: 2011-05-02T01:59:02+00:00
url: /2011/generate-openssh-public-key-for-sourceforge-with-puttygen/
categories:
  - SourceForge

---
SourceForgeはOpenSSHの公開鍵を登録しないと使えない機能が多いので
  
puttygen.exe でキーを生成して登録する。
  
ただputtyで使うキーがSSH形式でSourceForgeで使う形式のOpenSSHと違うためそのままでは登録できない。

なので
  
<http://hiromasaya.web.fc2.com/Windows/putty.html>
  
を参考にして

<pre>ssh-keygen -i -f id_rsa.pub > id_rsa_open_ssh.pub</pre>

でできた id\_rsa\_open_ssh.pub をエディタで開いてSourceForgeの入力フィールドにコピペで登録できました。

