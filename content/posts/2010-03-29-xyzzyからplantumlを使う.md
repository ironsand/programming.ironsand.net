---
title: xyzzyからPlantUMLを使う
author: 鉄
type: post
date: 2010-03-28T18:53:16+00:00
url: /2010/xyzzyからplantumlを使う/
categories:
  - xyzzy
tags:
  - PlantUML
  - UML
  - xyzzy

---
#### テキスト形式でUMLが書けるPlantUML

PlantUMLはテキスト形式でUMLを記述して画像に出力できるオープンソースのソフトウェアです。 UMLが書けるフリーソフトはいくつかありますが、テキストベースで記述できるのは大変ありがたいですね。

#### PlantUMLの具体例

サンプルをPlantUMLのサイト内から引用します。
  
<http://plantuml.sourceforge.net/classes.html>

[<img src="http://programming.ironsand.net/wp-content/uploads/2010/03/classes04-300x285.png" alt="" title="classes04" width="300" height="285" class="alignnone size-medium wp-image-44" srcset="http://programming.ironsand.net/wp-content/uploads/2010/03/classes04-300x285.png 300w, http://programming.ironsand.net/wp-content/uploads/2010/03/classes04-150x142.png 150w, http://programming.ironsand.net/wp-content/uploads/2010/03/classes04.png 463w" sizes="(max-width: 300px) 100vw, 300px" />][1]　
  
こんなUMLが以下の記述で作れちゃいます。<pre class=prettyprint>@startuml img/classes04.png abstract class AbstractList abstract AbstractCollection interface List interface Collection List <|-- AbstractList Collection <|-- AbstractCollection Collection <|- List AbstractCollection <|- AbstractList AbstractList <|-- ArrayList ArrayList : Object[] elementData ArrayList : size() enum TimeUnit TimeUnit : DAYS TimeUnit : HOURS TimeUnit : MINUTES @enduml</pre> 

#### PlantUMLのインストール

<http://plantuml.sourceforge.net/download.html>
  
から plantuml.jar をダウンロードしてください。
  
plantumlの実行にはJavaが必要になりますので、もしJavaがインストールされていなければ
  
<http://www.java.com/ja/download/>
  
からインストールを行ってください。

"Sequence Diagram" 以外の画像の出力、つまり普通に使うのであれば Graphviz もインストールする必要があります。
  
<http://graphviz.org/Download_windows.php>
  
からダウンロードしてインストールしてください。

以上でインストールは終了です。

#### xyzzyからPlantUMLを使う方法

さて、次は以下のコードを siteinit.l か .xyzzy に記述してください。 

<pre class="prettyprint cl">;;PlantUML
(setf *plant-uml* "java -jar \"S:/My Dropbox/home/bin/plantuml.jar\"")
(setf *graphvizdot* "S:/My Dropbox/home/bin/Graphviz/bin/dot.exe")
(defun plant-uml ()
  (interactive)
  (make-process (concat *plant-uml* " " (buffer-name (selected-buffer))
                        " -graphvizdot \"" *graphvizdot* "\"")
                :exec-directory (default-directory (selected-buffer))))</pre>

\*plant-uml\* と \*graphvizdot\* の値は適宜変更してください。
  
これでテキストファイルにUMLを記述して `M-x plant-uml` と入力すれば画像ファイルが出力されているはずです。

