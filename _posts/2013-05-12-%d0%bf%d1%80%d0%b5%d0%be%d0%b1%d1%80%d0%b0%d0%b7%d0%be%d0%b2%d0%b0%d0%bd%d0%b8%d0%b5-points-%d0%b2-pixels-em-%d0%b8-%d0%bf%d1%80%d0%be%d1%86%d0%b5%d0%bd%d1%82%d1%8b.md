---
title: Преобразование points в pixels, em и проценты
author: gearmobile
layout: post
permalink: /%d0%bf%d1%80%d0%b5%d0%be%d0%b1%d1%80%d0%b0%d0%b7%d0%be%d0%b2%d0%b0%d0%bd%d0%b8%d0%b5-points-%d0%b2-pixels-em-%d0%b8-%d0%bf%d1%80%d0%be%d1%86%d0%b5%d0%bd%d1%82%d1%8b/
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - points
---
На практике часто бывает необходимо преобразовать одни единицы измерения в другие. Наиболее часто это происходит при работе со шрифтами. Допустим, имеется ситуация, когда в Photoshop размер шрифта показывается в points. А при верстке макета в CSS правилах необходимо прописать размер шрифта в пикселях или процентах.

Как быть в данной ситуации? Если дело касается Photoshop, то можно установить в настройках этой программы, чтобы она выдавала размер шрифта в пикселях. Как это делается, рассказано в этой статье &#8211; &#8220;[В Photoshop шрифт в пунктах &#8211; как перевести в пиксели][1]&#8220;. Данный метод дает приближенное значение размера шрифта в пикселях, так как многое зависит от того, в каком разрешении был создан макет в Photoshop.

Другим способом, который может быть даже предпочтительнее, является ручной перевод из одних единиц измерения в другие. Чтобы не производить каждый раз такие преобразования, ниже представлена таблица, к которой даны наиболее распространенные размеры шрифтов в различных единицах измерения. Пользуясь этой таблицей, можно быстро перевести один размер в другой. В ней представлены единицы измерения point, pixel, em и проценты. То есть, четыре самых распространенных типа, три из которых наиболее часто применяются при создании CSS-правил.

## Таблица преобразования points в pixels, ems или проценты

<table style="width: 500px;" border="1">
  <tr>
    <th scope="col" width="83">
      Points
    </th>
    
    <th scope="col" width="81">
      Pixels
    </th>
    
    <th scope="col" width="60">
      Ems
    </th>
    
    <th scope="col" width="105">
      Проценты
    </th>
  </tr>
  
  <tr>
    <td>
      6pt
    </td>
    
    <td>
      8px
    </td>
    
    <td>
      0.5em
    </td>
    
    <td>
      50%
    </td>
  </tr>
  
  <tr>
    <td>
      7pt
    </td>
    
    <td>
      9px
    </td>
    
    <td>
      0.55em
    </td>
    
    <td>
      55%
    </td>
  </tr>
  
  <tr>
    <td>
      7.5pt
    </td>
    
    <td>
      10px
    </td>
    
    <td>
      0.625em
    </td>
    
    <td>
      62.5%
    </td>
  </tr>
  
  <tr>
    <td>
      8pt
    </td>
    
    <td>
      11px
    </td>
    
    <td>
      0.7em
    </td>
    
    <td>
      70%
    </td>
  </tr>
  
  <tr>
    <td>
      9pt
    </td>
    
    <td>
      12px
    </td>
    
    <td>
      0.75em
    </td>
    
    <td>
      75%
    </td>
  </tr>
  
  <tr>
    <td>
      10pt
    </td>
    
    <td>
      13px
    </td>
    
    <td>
      0.8em
    </td>
    
    <td>
      80%
    </td>
  </tr>
  
  <tr>
    <td>
      10.5pt
    </td>
    
    <td>
      14px
    </td>
    
    <td>
      0.875em
    </td>
    
    <td>
      87.5%
    </td>
  </tr>
  
  <tr>
    <td>
      11pt
    </td>
    
    <td>
      15px
    </td>
    
    <td>
      0.95em
    </td>
    
    <td>
      95%
    </td>
  </tr>
  
  <tr>
    <td>
      12pt
    </td>
    
    <td>
      16px
    </td>
    
    <td>
      1em
    </td>
    
    <td>
      100%
    </td>
  </tr>
  
  <tr>
    <td>
      13pt
    </td>
    
    <td>
      17px
    </td>
    
    <td>
      1.05em
    </td>
    
    <td>
      105%
    </td>
  </tr>
  
  <tr>
    <td>
      13.5pt
    </td>
    
    <td>
      18px
    </td>
    
    <td>
      1.125em
    </td>
    
    <td>
      112.5%
    </td>
  </tr>
  
  <tr>
    <td>
      14pt
    </td>
    
    <td>
      19px
    </td>
    
    <td>
      1.2em
    </td>
    
    <td>
      120%
    </td>
  </tr>
  
  <tr>
    <td>
      14.5pt
    </td>
    
    <td>
      20px
    </td>
    
    <td>
      1.25em
    </td>
    
    <td>
      125%
    </td>
  </tr>
  
  <tr>
    <td>
      15pt
    </td>
    
    <td>
      21px
    </td>
    
    <td>
      1.3em
    </td>
    
    <td>
      130%
    </td>
  </tr>
  
  <tr>
    <td>
      16pt
    </td>
    
    <td>
      22px
    </td>
    
    <td>
      1.4em
    </td>
    
    <td>
      140%
    </td>
  </tr>
  
  <tr>
    <td>
      17pt
    </td>
    
    <td>
      23px
    </td>
    
    <td>
      1.45em
    </td>
    
    <td>
      145%
    </td>
  </tr>
  
  <tr>
    <td>
      18pt
    </td>
    
    <td>
      24px
    </td>
    
    <td>
      1.5em
    </td>
    
    <td>
      150%
    </td>
  </tr>
  
  <tr>
    <td>
      20pt
    </td>
    
    <td>
      26px
    </td>
    
    <td>
      1.6em
    </td>
    
    <td>
      160%
    </td>
  </tr>
  
  <tr>
    <td>
      22pt
    </td>
    
    <td>
      29px
    </td>
    
    <td>
      1.8em
    </td>
    
    <td>
      180%
    </td>
  </tr>
  
  <tr>
    <td>
      24pt
    </td>
    
    <td>
      32px
    </td>
    
    <td>
      2em
    </td>
    
    <td>
      200%
    </td>
  </tr>
  
  <tr>
    <td>
      26pt
    </td>
    
    <td>
      35px
    </td>
    
    <td>
      2.2em
    </td>
    
    <td>
      220%
    </td>
  </tr>
  
  <tr>
    <td>
      27pt
    </td>
    
    <td>
      36px
    </td>
    
    <td>
      2.25em
    </td>
    
    <td>
      225%
    </td>
  </tr>
  
  <tr>
    <td>
      28pt
    </td>
    
    <td>
      37px
    </td>
    
    <td>
      2.3em
    </td>
    
    <td>
      230%
    </td>
  </tr>
  
  <tr>
    <td>
      29pt
    </td>
    
    <td>
      38px
    </td>
    
    <td>
      2.35em
    </td>
    
    <td>
      235%
    </td>
  </tr>
  
  <tr>
    <td>
      30pt
    </td>
    
    <td>
      40px
    </td>
    
    <td>
      2.45em
    </td>
    
    <td>
      245%
    </td>
  </tr>
  
  <tr>
    <td>
      32pt
    </td>
    
    <td>
      42px
    </td>
    
    <td>
      2.55em
    </td>
    
    <td>
      255%
    </td>
  </tr>
  
  <tr>
    <td>
      34pt
    </td>
    
    <td>
      45px
    </td>
    
    <td>
      2.75em
    </td>
    
    <td>
      275%
    </td>
  </tr>
  
  <tr>
    <td>
      36pt
    </td>
    
    <td>
      48px
    </td>
    
    <td>
      3em
    </td>
    
    <td>
      300%
    </td>
  </tr>
</table>

Отдельно стоит сказать, что не стоит путать point и punct (pt). Это разные единицы измерения.

#### P.S.

В процессе изучения CSS-типографии столкнулся с очень интересным ресурсом по преобразованию одних единиц измерения в другие &#8211; пиксели в em, проценты и пункты (pt) &#8211; `http://pxtoem.com/`:<figure id="attachment_750" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/05/px_to_em-600x420.jpg" alt="Конвертировать px в em" width="600" height="420" class="size-medium wp-image-750" />][2]<figcaption class="wp-caption-text">Конвертировать px в em</figcaption></figure> 

Помимо удобного способа конвертации одних единиц измерения в другие сервис предоставляет возможность получить готовый файл `normalize.css`, отредактированный службой `http://pxtoem.com/` под выбранное значение базового шрифта. Плюс к этому, в данный файл включены готовые стили для правильного вертикального ритма под выбранный размер шрифта. Супер! ))

Оцените статью:  
<span id="post-ratings-696" class="post-ratings" data-nonce="e4954a75ab"><img id="rating_696_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(696, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_696_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(696, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_696_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(696, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_696_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(696, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_696_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(696, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_696_text"></span></span><span id="post-ratings-696-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=698 "В Photoshop шрифт в пунктах - как перевести в пиксели"
 [2]: http://localhost:7788/third/wp-content/uploads/2013/05/px_to_em.jpg