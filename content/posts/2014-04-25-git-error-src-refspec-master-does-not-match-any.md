---
title: 'git の `error: src refspec master does not match any.`への対処'
author: 鉄
type: post
date: 2014-04-25T11:43:19+00:00
url: /2014/git-error-src-refspec-master-does-not-match-any/
categories:
  - Commands
  - git

---
<pre class="lang:sh decode:true " >$ git push -u origin master
error: src refspec master does not match any.</pre>

という見たことないエラーが出てビビる。

### 原因と対策

原因：コミットしてない
  
対策：コミットする

以上！

### 参考

[src refspec master does not match any when pushing commits in git &#8211; Stack Overflow][1]

