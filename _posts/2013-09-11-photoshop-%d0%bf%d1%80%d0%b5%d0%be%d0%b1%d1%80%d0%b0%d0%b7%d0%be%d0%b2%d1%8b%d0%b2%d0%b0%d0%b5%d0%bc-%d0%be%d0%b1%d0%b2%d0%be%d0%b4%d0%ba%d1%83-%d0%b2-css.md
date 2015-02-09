---
title: 'Photoshop &#8211; преобразовываем обводку в CSS'
author: gearmobile
layout: post
permalink: /photoshop-%d0%bf%d1%80%d0%b5%d0%be%d0%b1%d1%80%d0%b0%d0%b7%d0%be%d0%b2%d1%8b%d0%b2%d0%b0%d0%b5%d0%bc-%d0%be%d0%b1%d0%b2%d0%be%d0%b4%d0%ba%d1%83-%d0%b2-css/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 5
ratings_average:
  - 1.67
categories:
  - Photoshop для кодера
tags:
  - photoshop
---
При верстке из psd-макета можно столкнуться с такой ситуацией. Имеется какое-либо изображение, для которого в Photoshop создана обводка. Внешне это напоминает простую рамку для изображения. Но только внешне обводка похожа на рамку. На самом деле она накладывается на изображение поверх него.

У нас стоит задача преобразовать изображение с обводкой из psd-макета в html-код, используя при этом стилевые правила, где это допустимо. Само изображение преобразовать с помощью стилей невозможно &#8211; это картинка. А вот создать рамку (в данном случае это обводка) в помощью правил будет легко выполнить.

Осталось решить вопрос, как вырезать картинку из psd-макета, не трогая при этом обводку. Давайте посмотрим на фрагмент макета с интересующей нас картинкой и на панель слоев, отвечающих за ее прорисовку:<figure id="attachment_348" style="width: 575px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment.png" alt="Изображение с обводкой в Photoshop" width="575" height="235" class="size-full wp-image-348" />][1]<figcaption class="wp-caption-text">Изображение с обводкой в Photoshop</figcaption></figure> <figure id="attachment_349" style="width: 374px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer.png" alt="Слои, отвечающие за изображение и обводку в Photoshop" width="374" height="176" class="size-full wp-image-349" />][2]<figcaption class="wp-caption-text">Слои, отвечающие за изображение и обводку в Photoshop</figcaption></figure> 

На панели слоев видим два слоя &#8211; Layer 16 и Shape 14 copy. Именно они выполняют прорисовку картинки футболиста. На слое Shape 14 copy также видим эффекты, применяемые к этому слою. Если внимательно присмотреться к эффектам, то увидим надписи &#8220;Эффекты&#8221; &#8211; &#8220;Выполнить обводку&#8221;. Это как раз обводка, от которой нам необходимо избавиться, чтобы вырезать только саму фотографию.

Отлючаем эффект обводки. Для этого щелкаем мыщью на &#8220;глазике&#8221; &#8220;Эффекты&#8221; на слое Shape 14 copy. &#8220;Глазик&#8221; &#8220;потухает&#8221;, то есть эффект отключен. Смотрим на фотографию и видим, что обводка пропала:<figure id="attachment_350" style="width: 381px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-disabled.png" alt="Слой с отключенным эффектом обводки в Photoshop" width="381" height="215" class="size-full wp-image-350" />][3]<figcaption class="wp-caption-text">Слой с отключенным эффектом обводки в Photoshop</figcaption></figure> <figure id="attachment_351" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-disabled-600x235.png" alt="outline-fragment-disabled" width="600" height="235" class="size-medium wp-image-351" />][4]<figcaption class="wp-caption-text">outline-fragment-disabled</figcaption></figure> 

Теперь осталось вырезать изображение. Воспользуемся инструментом Photoshop под названием Crop. Выбираем его и вырезаем изображение. Затем сохраняем его для &#8220;Web и устройств &#8230;&#8221; в формате .jpg (наилучший вариант для фотографий).

Однако, нам еще необходимо узнать точные размеры и цвет обводки. Для этого опять воспользуемся слоями в Photoshop. Точнее &#8211; выберем слой Shape 14 copy и откроем его свойства. В списке эффектов выбираем &#8220;Обводка&#8221; и смотрим на правую часть, где представлены параметры, с помощью которых она выполнена:<figure id="attachment_352" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties-600x347.png" alt="Свойства обводки в Photoshop" width="600" height="347" class="size-medium wp-image-352" />][5]<figcaption class="wp-caption-text">Свойства обводки в Photoshop</figcaption></figure> 

Нам потребуются только два из них. Это толщина линии обводки &#8220;Размер&#8221; и цвет линии обводки &#8220;Цвет&#8221;. Также проверяем, что прозрачность (альфа-канал) для цвета обводки не используется, так как стоит &#8220;Непрозр.&#8221; равная 100%. Обводка выполнена сплошным цветом, так как на это указывает значение &#8220;Режим наложения: Нормальный&#8221;. Цвет обводки должен быть белым, но уточняем этот факт. Щелкаем на окошке &#8220;Цвет&#8221;:<figure id="attachment_353" style="width: 589px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties-color.png" alt="Цвет обводки в Photoshop" width="589" height="392" class="size-full wp-image-353" />][6]<figcaption class="wp-caption-text">Цвет обводки в Photoshop</figcaption></figure> 

Так все и есть &#8211; цвет равен #fff. Все готово для написания стилей CSS:

<pre>img.football { border:2px solid #fff; }</pre><figure id="attachment_354" style="width: 453px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-result.png" alt="outline-fragment-result" width="453" height="421" class="size-full wp-image-354" />][7]<figcaption class="wp-caption-text">outline-fragment-result</figcaption></figure> 

В результате получил иззображение с обводкой. Однако, в случае исполнения через стилевые правила CSS это будет не обводка, а чистая рамка. Размер изображения равен 62х59px. Добавляем к нему рамку размером 2px. Получаем реальный размер картинки на сайте 64x61px.

Средствами CSS на данный момент невозможно выполнить обводку, как на макете в Photoshop. Поэтому, если размер изображения критичен для шаблона, лучшим вариантом будет вырезание картинки вместе с обводкой.

P.S.  
Может быть так, что на самом слое в панели слоев эффект обводки не будет отображен:<figure id="attachment_355" style="width: 342px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-without-effects.png" alt="Отсутствие эффектов на слое в Photoshop" width="342" height="174" class="size-full wp-image-355" />][8]<figcaption class="wp-caption-text">Отсутствие эффектов на слое в Photoshop</figcaption></figure> 

В этом случае, для получения параметров обводки необходимо зайти в свойства слоя и дальше действовать также, как было описано в предыдущих шагах.

> Данное высказывание является несколько неточным. Эффекты слоя никуда не пропадают &#8211; они просто скрыты. Более подробное описание, как развернуть или скрыть отображение эффектов слоя в Photoshop можно почитать в статье &#8220;[Photoshop &#8211; скрытие и отображение эффектов слоя в палитре слоев][9]&#8220;

Оцените статью:  
<span id="post-ratings-346" class="post-ratings" data-nonce="1513b47ca5"><img id="rating_346_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(346, 1, '1 Star');" onmouseout="ratings_off(1.7, 2, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_346_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(346, 2, '2 Stars');" onmouseout="ratings_off(1.7, 2, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_346_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(346, 3, '3 Stars');" onmouseout="ratings_off(1.7, 2, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_346_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(346, 4, '4 Stars');" onmouseout="ratings_off(1.7, 2, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_346_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(346, 5, '5 Stars');" onmouseout="ratings_off(1.7, 2, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>1,67</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_346_text"></span></span><span id="post-ratings-346-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-disabled.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-disabled.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties-color.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-result.png
 [8]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-without-effects.png
 [9]: http://localhost:7788/third/?p=357 "Photoshop - скрытие и отображение эффектов слоя в палитре слоев"