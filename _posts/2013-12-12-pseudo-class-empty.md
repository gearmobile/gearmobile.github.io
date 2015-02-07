---
title: Краткая заметка по псевдо-классу :empty
author: gearmobile
layout: post
permalink: /pseudo-class-empty/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 9
ratings_average:
  - 4.5
categories:
  - Статьи по CSS
tags:
  - empty
---
Я люблю ту простоту, которую привносят CSS3-селекторы в таблицы стилей. В этой статье приведено краткое описание одного из моих любимых селекторов: псевдо-класса `:empty`.

## Что такое псевдо-класс :empty

Вот краткое описание, взятое из спецификации W3C:

> Псевдо-класс :empty относится к элементу, у которого нет потомков.

Звучит просто и понятно, не правда ли? Потому что это действительно так &#8211; псевдо-класс `:empty` применяется к элементам, которые полностью пустые; например, для пустого параграфа:

<pre><p>
  
</p>
</pre>

Или же пустые ячейки таблицы:

<pre><table>
  <tr>
    <td>
      
    </td>
          
  </tr>
      
</table>
</pre>

А вот к такому параграфу псевдо-класс `:empty` не применим, так как он не является пустым (внутри этого тега есть пробел, который является равноправным символом по сравнению со всеми остальными):

<pre><p>
  
</p>
</pre>

## Практическое применение :empty

Хорошо, но каким образом может быть полезен этот селектор?

Представим ситуацию, когда вы стилизуете таблицу и некоторые из ячеек этой таблицы не имеют данных внутри себя. Тогда вы можете применить к ним другие правила благодаря псевдо-классу `:empty`.

Давайте возьмем таблицу, которая создавалась мною ранее. Я собираюсь использовать те же самые таблицы стилей, но сделаю их более упрощенными. Также я собираюсь удалить содержимое из некоторых ячеек для того, чтобы сделать пример соответствующим статье.

Разметка будет выглядеть таким образом:

<pre><table>
  &lt;caption>A simple table&lt;/caption>
  
           
          
  
  <tr>
    <th scope="col" rowspan="2">
      Some headings
    </th>
              
    
    <th scope="col" colspan="4">
      More headings
    </th>
            
  </tr>
          
  
  <tr>
    <th scope="col">
      Great
    </th>
              
    
    <th scope="col">
      Brilliant
    </th>
              
    
    <th scope="col">
      Genius
    </th>
              
    
    <th scope="col">
      Good
    </th>
            
  </tr>       
        
  
        
          
  
  <tr>
    <th scope="row">
      Interesting totals
    </th>
              
    
    <td>
      155
    </td>
              
    
    <td>
      165
    </td>
              
    
    <td>
      70
    </td>
              
    
    <td>
      140
    </td>
            
  </tr>
        
  
        
          
  
  <tr>
    <th scope="row">
      Curious
    </th>
              
    
    <td>
      5
    </td>
              
    
    <td>
      35
    </td>
              
    
    <td>
      50
    </td>
              
    
    <td>
      15
    </td>
            
  </tr>
          
  
  <tr>
    <th scope="row">
      Awesome
    </th>
              
    
    <td>
      75
    </td>
              
    
    <td>
      90
    </td>
              
    
    <td>
      
    </td>
              
    
    <td>
      5
    </td>
            
  </tr>
          
  
  <tr>
    <th scope="row">
      Fabulous
    </th>
              
    
    <td>
      30
    </td>
              
    
    <td>
      
    </td>
              
    
    <td>
      20
    </td>
              
    
    <td>
      80
    </td>
            
  </tr>
          
  
  <tr>
    <th scope="row">
      Nice
    </th>
              
    
    <td>
      45
    </td>
              
    
    <td>
      40
    </td>
              
    
    <td>
      
    </td>
              
    
    <td>
      40
    </td>
            
  </tr>
  
        
  
      
</table>
</pre>

И вот, что я собираюсь добавить в таблицы стилей, для того чтобы отформатировать пустые ячейки таблицы:

<pre>tbody td:empty {
      background: #efefef;
    }
</pre>

А вот теперь пустые ячейки таблицы отформатированы [по-другому][1]! Мне кажется, что невозможно сделать это более простым способом.

Если вас этот селектор заинтересовал, то скажу, что он поддерживается всеми последними версиями браузеров Firefox, Safari, Chrome и Opera. И возможно, он работает в браузере Internet Explorer 9, наравне с остальными селекторами стандарта CSS3. 

Оцените статью:  
<span id="post-ratings-817" class="post-ratings" data-nonce="d1692db089"><img id="rating_817_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(817, 1, '1 Star');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_817_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(817, 2, '2 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_817_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(817, 3, '3 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_817_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(817, 4, '4 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_817_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(817, 5, '5 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>4,50</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_817_text"></span></span><span id="post-ratings-817-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://webdesignernotebook.com/examples/empty-selector.html "Empty Selector"