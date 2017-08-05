---
title: '[失敗] VPS上のUbuntu12.04にHeadlessなChromeかFirefoxをインストールするためにやったこと'
author: 鉄
type: post
date: 2014-03-27T14:23:54+00:00
url: /2014/install-headless-chrome-or-firefox-in-ubuntu-on-vps/
categories:
  - DigitalOcean
  - VPS
  - 失敗

---
phantomjs でzipファイルをダウンロードしたかったけど、ダウンロードオプションはまだ本体には取り込まれてないようなのでheadlessなChromeかFirefoxをVPSに入れて幸せな自動化処理生活を送ろうと思ったら全然うまく行きませんでした。

俺の苦労を返せ！

### やったこと

めんどくさいので説明は最低限で。

FirefoxとChrome、それにSelenium Webdriverで使うためのChromeDriverをインストール

<pre class="lang:sh decode:true " >apt-get install git unzip xvfb

echo 'deb http://ppa.launchpad.net/mozillateam/firefox-next/ubuntu precise main' &gt;&gt; /etc/apt/sources.list
echo 'deb-src http://ppa.launchpad.net/mozillateam/firefox-next/ubuntu precise main' &gt;&gt; /etc/apt/sources.list
apt-get install firefox

wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - 
echo "deb http://dl.google.com/linux/chrome/deb/ stable main" &gt;&gt; /etc/apt/sources.list.d/google.list
apt-get install google-chrome-stable

wget http://chromedriver.storage.googleapis.com/2.9/chromedriver_linux64.zip
unzip chromedriver_linux64.zip
mv chromdriver /usr/local/bin</pre>

この時点で

<pre class="lang:sh decode:true " >Xvfb :1 &
export DISPLAY=:1
firefox</pre>

すればFirefoxが立ち上がるはずだけどエラーが出てうまくいかない。
  
色々と検索してみるけど結局エラーを除去する方法は見つからず。

### Rubyとか

こちらはRubyを入れて`selenium-webdriver`を入れるまでのよくある感じのインストールメモ。DigitalOcean上のUbuntuにrootでログインしてそのままやってます。

<pre class="lang:sh decode:true " >apt-get install autoconf bison build-essential libssl-dev libyaml-dev libreadline6 libreadline6-dev zlib1g zlib1g-dev

git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' &gt;&gt; ~/.bash_profile
echo 'eval "$(rbenv init -)"' &gt;&gt; ~/.bash_profile
. ~/.bash_profile
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
rbenv install 2.1.1
rbenv global 2.1.1

gem install selenium-webdriver</pre>

他にもChromiumとか試してみたけど結局すべて失敗に終わりました。

