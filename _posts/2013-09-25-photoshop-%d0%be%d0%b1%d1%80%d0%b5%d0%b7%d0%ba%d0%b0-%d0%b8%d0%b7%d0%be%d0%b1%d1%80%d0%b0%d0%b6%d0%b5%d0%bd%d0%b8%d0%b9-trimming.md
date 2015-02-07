---
title: 'Photoshop &#8211; обрезка изображений (trimming)'
author: gearmobile
layout: post
permalink: /photoshop-%d0%be%d0%b1%d1%80%d0%b5%d0%b7%d0%ba%d0%b0-%d0%b8%d0%b7%d0%be%d0%b1%d1%80%d0%b0%d0%b6%d0%b5%d0%bd%d0%b8%d0%b9-trimming/
ratings_users:
  - 5
ratings_score:
  - 21
ratings_average:
  - 4.2
cleanretina_sidebarlayout:
  - default
categories:
  - Photoshop для кодера
tags:
  - photoshop
---
При нарезке макета часто возникает ситуация, когда необходимо вырезать изображение с прозрачным фоном. После того, как изображение вырезано и вставлено в новый документ для обработки, очень желательно подогнать размеры картинки так, чтобы она занимала минимальное место.

Вот тут на помощь и приходит инструмент &#8220;Trim&#8221; в Photoshop. С помощью него производится обрезка изображения на основе выбранного фильтра. В результате картинка получиться меньшего размера и только с полезным содержимым. Чтобы было понятнее, давайте разберем на примере.

Имеется некий макет, из которого необходимо вырезать логотип (очень частая операция). Первым делом, находим и определяем слои, из которых состоит логотип. Затем объединяем их в один слой и выделяем логотип на макете с помощью инструмента &#8220;Выделение&#8221;:<figure id="attachment_328" style="width: 549px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/select.png" alt="Выделенный логотип на шаблоне" width="549" height="304" class="size-full wp-image-328" />][1]<figcaption class="wp-caption-text">Выделенный логотип на шаблоне</figcaption></figure> 

Копируем его и вставляем в новый документ. На изображении хорошо видно, что выделение было произведено &#8220;на глаз&#8221; &#8211; имеют большие зазоры между границей выделения (штриховая линия) и границами самого изображения.

Это не совсем хорошо, так как фактически это пустая область, которая будет только занимать место. От нее необходимо избавиться. Первое, что нужно сделать, это отключить слой с фоном. Тогда изображение станет с прозрачным фоном. Об этом наглядно говорит то, что весь фон стал в виде шахматной клетки.

Затем переходим в меню &#8220;Image &#8211; Trim&#8221;:<figure id="attachment_329" style="width: 232px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/menu_trim.png" alt="menu trim" width="232" height="390" class="size-full wp-image-329" />][2]<figcaption class="wp-caption-text">menu trim</figcaption></figure> <figure id="attachment_330" style="width: 311px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/trim_options.png" alt="trim options" width="311" height="227" class="size-full wp-image-330" />][3]<figcaption class="wp-caption-text">trim options</figcaption></figure> 

В окне настроек устанавливаем радиокнопку в положение &#8220;Transparent Pixels&#8221;. В этом случае обрезка изображения будет производиться на основе поиска прозрачных пикселей, окружающих само изображение. Нажимаем ОК и получаем результат:<figure id="attachment_331" style="width: 383px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/trim_ready.png" alt="trim ready" width="383" height="154" class="size-full wp-image-331" />][4]<figcaption class="wp-caption-text">trim ready</figcaption></figure> 

То есть, Photoshop нашел все прозрачные пиксели, окружающие изображение, и удалил их так, чтобы не нарушить саму картинку. Границы изображения сузились и оказались точно подогнаными под границы самой картинки. Теперь ее можно сохранить и применять при последующей верстке.

Оцените статью:  
<span id="post-ratings-327" class="post-ratings" data-nonce="42f5b4381d"><img id="rating_327_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(327, 1, '1 Star');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_327_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(327, 2, '2 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_327_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(327, 3, '3 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_327_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(327, 4, '4 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_327_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(327, 5, '5 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>5</strong> votes, average: <strong>4,20</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_327_text"></span></span><span id="post-ratings-327-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/select.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/menu_trim.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/trim_options.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/trim_ready.png