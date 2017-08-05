---
title: WordPressでadd_filterで適用された関数の一覧を表示する
author: 鉄
type: post
date: 2013-12-10T14:39:05+00:00
url: /2013/show-all-filters-in-wordpress/
categories:
  - PHP
  - Wordpress

---
どんなフィルタが適用されてるか確認したかったので質問したら教えてもらえました。Stackexchangeの回答者様ありがとうございます。

[crayon lang=&#8221;php&#8221;]
  
<?php
function get_filters_for( $hook = '' ) {
    global $wp_filter;
    if( empty( $hook ) || !isset( $wp_filter[$hook] ) )
        return;

    return $wp_filter[$hook];
}
var_dump(get_filters_for( 'the_content' ));
[/crayon]



<h3>参考</h3> 

[How to check a filter are applied &#8211; WordPress Answers][1]

