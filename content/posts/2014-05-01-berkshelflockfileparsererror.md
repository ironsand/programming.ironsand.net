---
title: Berkshelf::LockfileParserError への対処
author: 鉄
type: post
date: 2014-04-30T19:13:31+00:00
url: /2014/berkshelf_lockfileparsererror/
categories:
  - Chef

---
`knife solo cook foo` とすると`Berkshelf::LockfileParserError`ってエラーが出てビビる。

### 対策

`rm Berkshelf.lock` で ロックファイルをを消したら治った。`.gitignore`に加えてたほうが良いのかな？ `Gemfile.lock`と同じく加えるかどうかに賛否両論ありそう。

