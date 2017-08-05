---
title: NokogiriとSelenium-WebDriverのxpathの違い
author: 鉄
type: post
date: 2014-05-04T01:39:37+00:00
url: /2014/difference-between-nokogiri-and-selenium-webdriver-about-xpath/
categories:
  - ruby

---
`Selenium-WebDriver`と`Nokogiri`で同じファイルを開いても違う`xpath`を書かないといけないとダメで少しハマったのでメモ。

## 違いの原因

同じHTMLを解析しても`Selenium-WebDriver`で`Chrome`や`Firefox`で開いた時は任意の要素である`tbody`が挿入されるために違いが発生します。

## 実際の例

例えば

<pre class="lang:xhtml decode:true " >&lt;table&gt;
      &lt;tr&gt;
        &lt;td&gt;&lt;/td&gt;
      &lt;/tr&gt;
    &lt;/table&gt;</pre>

とある時に

## Nokogiri の場合

<pre class="lang:ruby decode:true " >require 'nokogiri'
doc = Nokogiri::HTML(File.read("test.html"))
doc.xpath("//table/tr")</pre>

## Selenium WebDriver の場合

<pre class="lang:ruby decode:true " >require 'selenium-webdriver'
driver = Selenium::WebDriver.for :chrome
driver.get("file:///C:/Users/ironsand/test.html")
driver.find_element(:xpath, "//table/tbody/tr")</pre>

## 基本的な対策

大体の場合は`//table//tr`とどちらにも対応できるように書いたらいいわけですが、汚いHTMLを解析するときに

`//tr/td/font[contains(text(), 'Keyword')]/../../following-sibling::tr[3]/td`

な感じで正確なタグの数が必要になることがあるのでそういう時に気をつけましょう。

## 参考

[ruby &#8211; How to get element that have same parent and n th different position by xpath &#8211; Stack Overflow][1]

