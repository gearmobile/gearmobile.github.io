---
title: 'CSS &#8211; текст в логотипе HTML-шаблона'
author: gearmobile
layout: post
permalink: /css-%d1%82%d0%b5%d0%ba%d1%81%d1%82-%d0%b2-%d0%bb%d0%be%d0%b3%d0%be%d1%82%d0%b8%d0%bf%d0%b5-html-%d1%88%d0%b0%d0%b1%d0%bb%d0%be%d0%bd%d0%b0/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Статьи по CSS
tags:
  - css
---
Совсем коротенькая заметка, посвященная такому приему, как помещение текста в логотип. В чем заключается вопрос? В каждом psd-макете имеется логотип для будущего сайта. Как правило, дизайнер старается сделать его запоминающимся, неординарным. Чтобы пользователю он бросался в глаза, оставил в его мозгу память о посещенном сайте. Поэтому подобные логотипы делаются вычурными, с графикой, нестандартными шрифтами.

При верстке подобный логотип можно сделать почти полностью на CSS, но это займет много времени. И, как правило, верстальщики так не делают. Обычно логотип сайта вырезается из psd-макета одной картинкой и вставляется в код или как фоновое изображение (предпочтительный вариант, так как логотип меняется очень редко), или же, как картинка в самом HTML-документе (такой подход на сегодняшний день не приветствуется из-за правил семантики).

Однако помимо правил семантики HTML, существует еще и такая вещь, как SEO. Без этой технологии не проживет ни один сайт на сегодняшний день, если он хочет быть известным, конечно. А если ему достаточно быть широко известным в узких кругах &#8211; тогда можно и забыть о ней. Поэтому, при верстке HTML-шаблона вырезанную картинку-логотип верстальщик оборачивает в ссылку (ибо логотип всегда должен быть ссылкой), которую в свою очередь оборачивает в заголовок первого уровня H1. Тег h1 должен быть один на всей странице, и это один из самых главных тегов для SEO &#8211; по нему поисковые машины находят сам сайт.

Но для Google, Yandex и других систем наиболее важной составляющей сайта является текст. Поэтому внутрь конструкции заголовок + ссылка + картинка нужно вставить сам тест, который дублирует название сайта в логотипе. Например, таким образом:<figure id="attachment_377" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/text-in-logo-600x286.png" alt="Текст в логотипе сайта" width="600" height="286" class="size-medium wp-image-377" />][1]<figcaption class="wp-caption-text">Текст в логотипе сайта</figcaption></figure> 

Но тогда возникает небольшая проблема &#8211; текст ссылки появляется в логотипе, когда браузер отрисовывает картинку. Чтобы было понятно, о чем идет речь, привожу картинку ниже:<figure id="attachment_378" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/text-in-logo-shablon-600x237.png" alt="Текст ссылки внутри логотипа" width="600" height="237" class="size-medium wp-image-378" />][2]<figcaption class="wp-caption-text">Текст ссылки внутри логотипа</figcaption></figure> 

Некрасиво, конечно. И совсем не то, что требуется. Как же убрать эту ссылку? Выход решается одной строчкой, с помощью свойства text-indent. Тексту задаем это свойство так, чтобы спрятать его из видимой части окна браузера.

Пример кода, решающего такую задачу, показан ниже:<figure id="attachment_379" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/text-indent-600x286.png" alt="Убрать текст из окна браузера" width="600" height="286" class="size-medium wp-image-379" />][3]<figcaption class="wp-caption-text">Убрать текст из окна браузера</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-375" class="post-ratings" data-nonce="cf6a4397fd"><img id="rating_375_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(375, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_375_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(375, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_375_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(375, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_375_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(375, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_375_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(375, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_375_text"></span></span><span id="post-ratings-375-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

n

 [1]: http://localhost:7788/third/wp-content/uploads/2013/09/text-in-logo.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/09/text-in-logo-shablon.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/09/text-indent.png