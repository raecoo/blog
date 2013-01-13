---
layout: post
title: String truncate in PHP
---

<pre><code>  function truncate($str,$len,$suffix = false) 
  { 
    if (strlen($str) <= $len ) 
    { 
      return $str; 
    }else { 
      $i = 0; 
      while ($i < $len) 
      { 
        $tmp = substr($str,$i,1); 
        if ( ord($tmp) >=224 ){ 
          $tmp = substr($str,$i,3); 
          $i = $i + 3; 
        }elseif( ord($tmp) >=192 ){ 
          $tmp = substr($str,$i,2); 
          $i = $i + 2; 
        }else{ 
          $i = $i + 1; 
        } 
        $strLast[] = $tmp; 
      } 
      $strLast = implode("",$strLast); 
      if($suffix){ 
        $strLast .= "..."; 
      } 
      return $strLast; 
    } 
  }</code></pre>
