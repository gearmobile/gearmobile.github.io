---
title: 'Photoshop &#8211; определить прозрачность слоя на макете'
author: gearmobile
layout: post
permalink: /photoshop-%d0%be%d0%bf%d1%80%d0%b5%d0%b4%d0%b5%d0%bb%d0%b8%d1%82%d1%8c-%d0%bf%d1%80%d0%be%d0%b7%d1%80%d0%b0%d1%87%d0%bd%d0%be%d1%81%d1%82%d1%8c-%d1%81%d0%bb%d0%be%d1%8f-%d0%bd%d0%b0-%d0%bc%d0%b0/
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - Photoshop для кодера
tags:
  - photoshop
---
Часто при верстке psd-макета приходится сталкиваться с ситуацией, когда дизайнер применяет полупрозрачность в слое. Сегодня это достаточно стандартный прием, так как средства CSS позволяют легко передать в коде полупрозрачность любого цвета. Осуществляется это с помощью свойства rgba, где последняя буква а обозначает альфа-канал. Благодаря этому альфа-каналу и передается полупрозрачность.

Хорошо, с этим разобрались &#8211; легко можно передать в помощью CSS прозрачность. Но вот при верстке psd-макета как узнать, какое значение прозрачности задал дизайнер. Оказывается, все достаточно просто и не нужно лезть куда-то вглубь, в свойства.

Допустим, есть пример psd-макета, в котором есть слои с полупрозрачностью:<figure id="attachment_334" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/opacity-600x470.jpg" alt="Макет с полупрозрачностью в Photoshop" width="600" height="470" class="size-medium wp-image-334" />][1]<figcaption class="wp-caption-text">Макет с полупрозрачностью в Photoshop</figcaption></figure> 

Видим, что на нем есть два участка, где художник применил полупрозрачность. Верхняя часть, где будет располагаться шапка будущего сайта; нижняя часть, в которой будет находиться подвал сайта. С цветом можно определиться сразу, &#8220;на глаз&#8221; &#8211; это черный цвет #000.

Если вдруг не уверены с правильностью определения цвета, то можно продублировать нужный слой в отдельный документ и ткнуть в него &#8220;пипеткой&#8221;:<figure id="attachment_335" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/color-600x467.jpg" alt="Цвет продублированного слоя в Photoshop" width="600" height="467" class="size-medium wp-image-335" />][2]<figcaption class="wp-caption-text">Цвет продублированного слоя в Photoshop</figcaption></figure> 

Почему нужно обязательно дублировать слой? А вы попробуйте &#8220;ткнуть&#8221; пипеткой в интересующий слой на самом макете. Вы никогда не получите одного и того же цвета, и ни разу &#8211; черного. Так и должно быть, так как наш слой полупрозрачный, сквозь который проступает еще один слой &#8211; с фоновой картинкой. Поэтому лучше продублировать слой и там уже проверять цвет заливки.

Но вернемся к вопросу, ради которого и затевалась эта небольшая статья. Наверное, внимательные читатели уже ответили для себя на него, посмотрев на первую картинку. Последовательность действий в этом случае стандартная &#8211; открываем палитру слоев в Photoshop. Выбираем инструмент Move Tool (V) и ткнем мышью на нужном слое.

Если Photoshop настроен правильно, то искомый слой автоматически выделиться в палитре (как на рисунке). Переводим взгляд в верхний правый угол палитры и видим там небольшое окошко с названием Opacity (Полупрозрачность).

Это как раз то, что нам нужно. В этом окошке показывается полупрозрачность, с которой дизайнер нарисовал этот слой. В моем случае она равна 90%. Это значение и нужно использовать при создании CSS-кода.

Например, так:

<pre>background-color: rgba(0,0,0, 0.9);</pre>

Оцените статью:  
<span id="post-ratings-333" class="post-ratings" data-nonce="b16b306f5d"><img id="rating_333_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(333, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_333_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(333, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_333_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(333, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_333_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(333, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_333_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(333, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_333_text"></span></span><span id="post-ratings-333-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/opacity.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/color.jpg