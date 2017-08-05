---
title: 既に存在するindexにunique制限をかけるmigrationの書き方。
author: 鉄
type: post
date: 2013-12-09T10:22:53+00:00
url: /2013/how-to-add-unique-constraint-to-already-existing-index-by-migration/
categories:
  - Rails
  - ruby

---
そのまま unique 条件付の index を追加しようとするとエラーになるので
  
まず既にある index を削除してから追加しましょう。

[crayon title=&#8221;db/migrate/add\_unique\_constraint.rb&#8221;]
    
def change
      
remove\_index :editabilities, [:user\_id, :list_id]
      
add\_index :editabilities, [:user\_id, :list_id], unique: true
    
end
  
[/crayon]

### 参考

[ruby on rails &#8211; How to add `unique` constraint to already existing index by migration &#8211; Stack Overflow][1]

