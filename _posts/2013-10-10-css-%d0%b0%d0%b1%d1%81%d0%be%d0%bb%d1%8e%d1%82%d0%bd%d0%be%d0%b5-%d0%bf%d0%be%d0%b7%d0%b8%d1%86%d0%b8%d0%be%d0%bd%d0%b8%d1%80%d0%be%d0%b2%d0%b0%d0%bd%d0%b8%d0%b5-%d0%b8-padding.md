---
title: 'CSS &#8211; абсолютное позиционирование и padding'
author: gearmobile
layout: post
permalink: /css-%d0%b0%d0%b1%d1%81%d0%be%d0%bb%d1%8e%d1%82%d0%bd%d0%be%d0%b5-%d0%bf%d0%be%d0%b7%d0%b8%d1%86%d0%b8%d0%be%d0%bd%d0%b8%d1%80%d0%be%d0%b2%d0%b0%d0%bd%d0%b8%d0%b5-%d0%b8-padding/
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
  - css
  - padding
---
При верстке одного макета столкнулся с таким вопросом. Имеется блок-баннер, у которого заданы границы border и padding. Внутри этого блока располагается блок с текстом. Этот блок позиционируется абсолютно относительно своего блока-родителя.

При задании CSS-параметров абсолютного позиционирования у меня возник вопрос &#8211; отчего же отсчитывается позиционирование для внутреннего блока? От границы border или padding внешнего блока?

По памяти вспомнить не смог, поэтому быстро накидал обрацез-пример, чтобы увидеть, как это происходит на самом деле. Ниже привожу красочную картинку, в которой и так понятно все, без слов:<figure id="attachment_245" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/pos-abs-600x332.png" alt="Абсолютное позиционирование" width="600" height="332" class="size-medium wp-image-245" />][1]<figcaption class="wp-caption-text">Абсолютное позиционирование</figcaption></figure> 

Ниже все же в двух словах опишу картинку.

Итак:</p> 

  * - внешний блок div имеет границу border шириной 10px, отступ (я его называю так) padding размером 20px и относительное позиционирование;
  * - внутренний блок div имеет абсолютное позиционирование &#8211; top:40px и left:40px.

Так вот, внутренний блок позиционируется абсолютно внутри внешнего блока-родителя по его границе. При этом отступ padding роли не играет, он не учитывается совсем. Вот и выяснил для себя этот вопрос.

Оцените статью:  
<span id="post-ratings-244" class="post-ratings" data-nonce="1ce72f5abc"><img id="rating_244_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(244, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_244_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(244, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_244_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(244, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_244_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(244, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_244_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(244, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_244_text"></span></span><span id="post-ratings-244-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/pos-abs.png