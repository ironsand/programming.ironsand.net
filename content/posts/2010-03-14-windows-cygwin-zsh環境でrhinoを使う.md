---
title: Windows(cygwin+zsh)環境でRhinoを使う
author: 鉄
type: post
date: 2010-03-14T02:16:35+00:00
url: /2010/windows-cygwin-zsh環境でrhinoを使う/
categories:
  - javascript
tags:
  - JAVA
  - javascript

---
#### Rhinoとは何か？

javascript を記述するときに毎回htmlファイルを作る作業が手間なので何か方法がないか探してみた。 どうやら、JAVAで書かれたjavascript実装のRhinoでやりたい事ができるらしい。

<blockquote cite="https://developer.mozilla.org/ja/Rhino">
  <p>
    <a href="https://developer.mozilla.org/ja/Rhino">Rhino &#8211; MDC</a>
  </p>
  
  <p>
    Rhino はすべてが Java で記述された JavaScript のオープンソースな実装です。それは一般的には、Java アプリケーション環境へ組み込まれて、エンドユーザーによるスクリプトの記述が可能になります。
  </p>
</blockquote>

#### Rhinoのインストール方法

J2SE 6には標準で入っているらしいがEverythingで探しても見つからないので今回は <http://www.mozilla-japan.org/rhino/download.html> からダウンロードして使うことにする。 

ダウンロード+解凍して適当なディレクトリに移動する(私の環境ではSugarSyncで共有してるディレクトリ配下のX:\sugarsync\bin\rhino1_7R2)。 スペースや日本語の文字列を含まない場所に置くのが無難だろう。 次に CLASSPATH を設定する。<pre class=prettyprint>CLASSPATH=x:\\sygarsync\\bin\\rhino1_7R2\\js.jar export CLASSPATH # /cygdrive/x/～ の形式では java が認識しない。</pre> 

これでインストールは完了したので

<pre>java org.mozilla.javascript.tools.shell.Main</pre>

と入力すればインタープリタが起動する。

#### zshrcでエイリアスの設定

しかし毎回これを打つのはあまり現実的ではないため ~/zshrc で alias を設定しておくと良い。<pre class=prettyprint>alias js="java org.mozilla.javascript.tools.shell.Main"</pre> 

インタープリタを呼び出さずに直接実行することや、jsファイルを直接指定して実行することもできる。<pre class=prettyprint>js -e "print('hello')" js -f hello.js</pre> 

これでjavascriptの動作をちょっと確認したいときに簡単に動かせるようになったし、JAVAで実装されているため、JAVAのクラスをjavascript内部で呼び出したりもできるようだ。 色々と遊んでいこうと思う。

