---
title: Раздвижной фон (sliding doors) сайта с помощью CSS
author: gearmobile
layout: post
permalink: /%d1%80%d0%b0%d0%b7%d0%b4%d0%b2%d0%b8%d0%b6%d0%bd%d0%be%d0%b9-%d1%84%d0%be%d0%bd-sliding-doors-%d1%81%d0%b0%d0%b9%d1%82%d0%b0-%d1%81-%d0%bf%d0%be%d0%bc%d0%be%d1%89%d1%8c%d1%8e-css/
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
Просматривал один из видеокурсов по верстке сайта и разворачиванию его на CMS Joomla. И столкнулся с такой вещью, как вложенность слоев. В видеокурсе был рассмотрен очень наглядный и интересный пример, как с помощью вложенных слоев можно создавать раздвижной фон сайта. Сперва было немного непонятно, но потом все встало на свои места. До этого момента, разбирая готовые примеры верстки, никогда не сталкивался с таким приемом.

Конечно, можно сохранить где-нибудь этот видеоурок и просматривать его, если забыл какие-то моменты. Но показанный в нем прием мне так понравился, что я решил описать его сам, своими собственными словами. Более того, благодаря этому приему для меня &#8220;открылась&#8221; возможность работы с вложенными слоями. Оказалось, это достаточно простое и эфективное решение, которое можно применять при верстке на практике. И, как мне кажется, данное решение является 100%-но кроссбраузерным.

И так. Имеется сайт с неоднородным фоном. Сайт планируется создавать с подвалом, прижатым книзу. Так как фон неоднородный, то необходимо сделать так, чтобы он подвижным. Он будет состоять из двух частей &#8211; верхней части, неподвижно закрепленной вверху страницы. И нижней части, которая будет всегда прижата книзу сайта и перемещаться вместе с подвалом вверх-вниз взависимости от величины контента в средней части:<figure id="attachment_225" style="width: 512px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sliding-fon.png" alt="Неоднородный фон страницы" width="512" height="517" class="size-full wp-image-225" />][1]<figcaption class="wp-caption-text">Неоднородный фон страницы</figcaption></figure> 

Как будем поступать. Выделить и вырезать фон из psd-макета не составляет проблем. Затем сохраняем выделенный фон в виде jpeg-файла. После этого нужно разрезать полученную картинку пополам. В результате получиться две части одного фона &#8211; верхняя и нижняя. Верхнюю разместим вверху страницы и закрепим там. А нижнюю часть поместим вниз сайта и сделаем так, чтобы она была постоянно прижата к нему. И так, выделили, разрезали и сохранили. Все у нас получилось.

Теперь начинается самое интересное. Будем создавать каркас сайта и в нем реализовывать нашу задумку. Но для начала набросаем схему-каркас сайта. Она очень проста и создана мною в качестве примера:<figure id="attachment_226" style="width: 537px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/karkas.png" alt="Каркас будущей страницы" width="537" height="324" class="size-full wp-image-226" />][2]<figcaption class="wp-caption-text">Каркас будущей страницы</figcaption></figure> 

Смотрим и видим пять слоев на div&#8217;ах, которые вложены один в другой. Первый слой с классом .wrap является оберткой, на которую возложена задача центрирования страницы и задания ей определенной ширины. Второй слой с классом .fon-bot предназначен для размещения нем фонового изображения, в частности &#8211; нижней части фонового изображения сайта. В этот слой вложен еще один слой с классом .fon-top, в котором расположена в качестве фона верхняя часть картинки. И, наконец, самый последний и глубоковложенный слой &#8211; это будущий контент сайта с классом .content.

HTML-каркас создан. Теперь нужно прописать стили для него, чтобы он &#8220;ожил&#8221;. Делаю так:<figure id="attachment_227" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-karkas-600x347.png" alt="Раздвижной фон страницы" width="600" height="347" class="size-medium wp-image-227" />][3]<figcaption class="wp-caption-text">Раздвижной фон страницы</figcaption></figure> 

Слой .wrap &#8211; тут все понятно без лишних слов. Далее &#8211; слой .fon-bot. В нем задается фоновая картинка, которая прижимается с помощью свойства background-position в правый нижний угол блока. Посмотрите на значения этого свойства: 100% 100%. Это как раз и задает фоновому изображению положение в правом нижнем углу. Фактически, теперь она будет постоянно прижата книзу блока .fon-bot, что нам и требовалось.

С точностью до наоборот поступаем с блоком .fon-top. Также устанавливаем для него фоновое изображение, но позиционируем его в левом верхнем углу с помощью значений 0 0. Теперь картинка будет всегда прижата кверху этого блока. Фактически, поставленная перед нами задача уже выполнена.

Но для наглядности в пример добавлен еще один, пятый блок .content. На практике он выполняет функцию контейнера для всего содержимого страницы сайта. Вставим внутрь этого слоя фоновое изображение и зададим ему минимальную высоту, которая превышает высоту блоков .fon-top и .fon-bot в сумме (точнее &#8211; высоту фоновых картинок обоих слоев). Также отцентруем фоновую картинку блока .content.

В итоге получим следующий результат (чтобы пример веселее смотрелся, в качестве фоновых картинок вставил красоток-сестренок Марианну и Камиллу Давалос):<figure id="attachment_228" style="width: 416px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/background-result-416x600.png" alt="Раздвижной фон страницы" width="416" height="600" class="size-medium wp-image-228" />][4]<figcaption class="wp-caption-text">Раздвижной фон страницы</figcaption></figure> 

При увеличении значения min-height слоя .content верхняя и нижняя картинки будут разъезжаться, а при уменьшении &#8211; съезжаться. Если не ошибаюсь, описанный мною способ называется методом &#8220;раздвижных дверей&#8221; (сам такой метод не изучал, но встречал в книгах по CSS такое упоминание.)

Полезным для себя вынес такой прием, как работа с неоднородным фоном страницы.

Оцените статью:  
<span id="post-ratings-224" class="post-ratings" data-nonce="198cddfaba"><img id="rating_224_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(224, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_224_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(224, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_224_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(224, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_224_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(224, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_224_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(224, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_224_text"></span></span><span id="post-ratings-224-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/sliding-fon.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/karkas.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/css-karkas.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/background-result.png