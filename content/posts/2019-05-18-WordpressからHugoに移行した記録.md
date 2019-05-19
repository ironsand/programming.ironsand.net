---
title: WordpressからHugoに移行した記録
author: 鉄
type: post
date: 2019-05-18
url: /2019/WordpressからHugoに移行した記録/
categories:
  - Hugo
---

## インストール方法

Macなら特に何も面倒くさいことをせずに

```
brew update
brew install hugo
```

でOKです。

無事インストールできたか確認ついでにバージョンも表示。

```.sh
 % hugo version
Hugo Static Site Generator v0.55.5/extended darwin/amd64 BuildDate: unknown
```

## 初期設定と動作確認

まずこのサイトの置き場所のためにディレクトリを`~/www/programming.ironsand.net`を作って、そこに`cd`で移動。

```.sh
% hugo new site .
Congratulations! Your new Hugo site is created in /Users/ironsand/www/programming.ironsand.net.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/, or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

「テーマを https://themes.gohugo.io/ から探してくるか自分で作ってね。」と言われたので

[Lithium](http://themes.gohugo.io/hugo-lithium-theme/) を使うことにしました。

```.sh
% cd themes
git clone https://github.com/jrutheiser/hugo-lithium-theme
```

そして、設定ファイルの`config.toml`を https://github.com/jrutheiser/hugo-lithium-theme/blob/master/exampleSite/config.toml を見ながら修正。

```./config.toml

baseurl = "http://programming.ironsand.net"
languageCode = "ja-JP"
title = "答えを知りたい"
theme = "hugo-lithium-theme"
googleAnalytics = ""
disqusShortname = ""

[permalinks]
    post = "/:year/:month/:day/:title/"
    page = "/:title/"

[[menu.main]]
    name = "About"
    url = "/about/"
[[menu.main]]
    name = "GitHub"
    url = "https://ironsand.github.com"
[[menu.main]]
    name = "Twitter"
    url = "https://twitter.com/ironsand"

[params]
    description = "答えを知りたい"

    [params.logo]
    url = "logo.png"
    width = 50
    height = 50
    alt = "Logo"
```

### ようこそページを作成

```.sh
 % hugo new post/welcome.md
/Users/ironsand/www/programming.ironsand.net/content/post/welcome.md created
```

そしてできたページを適当に編集します。

```content/posts/welcome.md
+++
date = "2017-03-24T22:06:35+08:00"
title = "welcome"

+++

Welcome!
```

`draft= true`という記述があるので削除しましょう。これがあると下書き扱いなので表示されません。

### サーバーを動かす

あとはサーバーを立てて`localhost:1313`にアクセスして無事に画面が表示されれば初期設定は完了です。

```.sh
 % hugo server -w
```

## Wordpress のデータをHugoに移行

Wordpress はさくらのレンタルサーバに置いてるので、`ssh` でサーバーに繋いで

```.sh
cd ~/www/programing.ironsand.net/wp-content/plugins
wget https://github.com/SchumacherFM/wordpress-to-hugo-exporter/archive/master.zip
unzip master.zip
```

とするとWordpressの管理画面の`プラグイン`に`WordPress to Hugo Exporter`ができてるので有効化します。

###  `syntax error, unexpected '[' in ` エラーが出る。

古いバージョンの`php`では配列の`[]`記法がサポートされてないようなのでこんなエラーが出ました。

```.php
Parse error: syntax error, unexpected '[' in /home/ironsand/www/programming.ironsand.net/wp-content/plugins/wordpress-to-hugo-exporter-master/hugo-export.php on line 133
```

[さくらのサーバコントロールパネル](https://secure.sakura.ad.jp/rscontrol/) にログインして`PHPのバージョン選択`からPHPのバージョンを5系最新の`5.6`に上げれば正常に有効化できました。

### zipファイルでダウンロード

拡張が正常に有効化できたら`ツール`に`Export to Hugo`というメニューができてるので実行します。私の環境では5秒ほどでダウンロードダイアログが出てきたので`zip`ファイルをダウンロードしましょう。

### ファイルの移行

`zip`ファイルを展開すると`post`フォルダの中にMarkdown形式の記事が入ってますので全てHugoの`contents/posts/`ディレクトリの中に入れてしまえば移行は完了です。ただ使っているプラグインによっては多少の変更は必要になります。

## サーバーにアップロード

サーバーは忍者ホームページを使うので `programming.ironsand.net`というプロジェクトを作成しました。
次に`config.toml`に`publishDir = "docs"`を追記してHUGOのHTMLの出力先をGithubの標準に合わせます。

Github上のプロジェクトの`Settings`->`Github Pages`で`Source`の項目を`None(Disable Github Pages)`から`master branch　/docs folder`に変更します。

これで数分待てばサーバーにアップロードできたのですが、この時点ではURLが`https://ironsand.github.io/programming.ironsand.net/`になってしまってるのでドメインの設定をします。

### 参考
https://gohugo.io/hosting-and-deployment/hosting-on-github/

## 独自ドメインの設定

さっき開いた`Github Pages`の設定項目に`Custom domain`があるのでそこに`programming.ironsand.net`と自分の使いたいドメインを入力して`Save`します。この時点では当然以下のようなエラーが出ますが無視します。

> Domain does not resolve to the GitHub Pages server. For more information, see https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/.
