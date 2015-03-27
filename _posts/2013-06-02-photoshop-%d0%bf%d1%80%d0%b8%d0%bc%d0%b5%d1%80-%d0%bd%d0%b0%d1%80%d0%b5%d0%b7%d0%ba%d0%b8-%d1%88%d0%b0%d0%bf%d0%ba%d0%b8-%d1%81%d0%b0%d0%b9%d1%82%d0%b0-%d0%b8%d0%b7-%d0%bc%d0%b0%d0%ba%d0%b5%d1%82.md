---
title: 'Photoshop &#8211; пример нарезки шапки сайта из макета'
author: gearmobile
layout: post
permalink: /photoshop-%d0%bf%d1%80%d0%b8%d0%bc%d0%b5%d1%80-%d0%bd%d0%b0%d1%80%d0%b5%d0%b7%d0%ba%d0%b8-%d1%88%d0%b0%d0%bf%d0%ba%d0%b8-%d1%81%d0%b0%d0%b9%d1%82%d0%b0-%d0%b8%d0%b7-%d0%bc%d0%b0%d0%ba%d0%b5%d1%82/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Photoshop для кодера
tags:
  - photoshop
---
Столкнулся с такой трудностью, как вырезать логотип из шапки макета. Проблема заключалась в том, что один слой накладывался на другой. Решение было найдено благодаря помощи форума htmlbook. Итак, имеется фрагмент шапки. Из нее необходимо вырезать будущий логотип, который должен представлять из себя файл с прозрачным фоном, значком флага и надписью Formula:<figure id="attachment_467" style="width: 492px;" class="wp-caption aligncenter">

[<img class="size-full wp-image-467" alt="Фрагмент шапки сайта" src="http://localhost:7788/third/wp-content/uploads/2013/06/header_maket.png" width="492" height="289" />][1]<figcaption class="wp-caption-text">Фрагмент шапки сайта</figcaption></figure> 

Выбираем инструмент &#8220;Перемещение&#8221;, проверяем, что в панели отмечен флажок &#8220;Автовыбор: Группы слоев&#8221;. Поочередно кликаем в шапке на значке флага, надписи Formula и фоновой заливке, одновременно отмечая, какие слои отвечают за прорисовку каждого элемента макета. В результате в панели слоев видим три слоя, которые в сумме составляют шапку: Formula, Layer26, Shape2:<figure id="attachment_468" style="width: 372px;" class="wp-caption aligncenter">

[<img class="size-full wp-image-468" alt="Слои, отрисовывающие логотип шапки" src="http://localhost:7788/third/wp-content/uploads/2013/06/header_layers.png" width="372" height="471" />][2]<figcaption class="wp-caption-text">Слои, отрисовывающие логотип шапки</figcaption></figure> 

Для дальнейшей работы с данными слоями наиболее удобным вариантом будет скопировать их в отдельный новый документ. Этим достигаются две цели: во-первых, с отдельно выделенными из документа слоями удобнее работать; во-вторых, таким образом мы обезопасим себя от случайного непреднамеренного изменения исходного документа. И хотя в Photoshop есть инструмент &#8220;История&#8221;, все же данный способ мне кажется более удобным.

Итак, выделяем все три слоя. Для этого зажимаем клавишу Ctrl и поочередно кликаем мышью на слоях Formula, Layer26, Shape2. Затем переходим в меню &#8220;Слои &#8211; Дубликат слоев&#8230;&#8221;. Открывается небольшое диалоговое окно &#8220;Дубликат слоев&#8221;, в котором выбираем назначение &#8220;Документ &#8211; Новый&#8221; и нажимаем ОК. Выбранные нами слои продублируются (создадутся копии) в новый документ Photoshop, который автоматически откроется в новой вкладке &#8220;Безимени-1&#8243;.

Шахматка в фоне означает, что фоновый слой прозрачный. Уберем лишние прозрачные пиксели фона, которые нам ни к чему. Но перед этим еще раз проанализируем три продублированных слоя. Слой Formula представляет из себя текст с эффектом тени. При вырезании логотипа мы оставим его как есть &#8211; вместе с тенью. В этом случае текст &#8220;попадет&#8221; в шапку будущего шаблона сайта неизменным &#8211; нарисованным тем шрифтом, который выбрал дизайнер. Это полностью нас устраивает.

Следующий слой &#8211; это значок флага. Его мы также должны перенести в шапку шаблона. Третий слой &#8211; фоновая заливка с градиентом. На панели слое мы видим, что оба последних слоя взаимосвязаны друг с другом &#8211; Layer26 и Shape2. Помимо этого, к слою Shape2 применены эффекты &#8211; внутренняя и внешняя тени. От них мы можем легко избавиться, так они свободно реализуются с помощью стилевых правил CSS, которые мы пропишем в будущем шаблоне. Поэтому отключаем их, щелкнув на &#8220;глазе&#8221; напротив надписи &#8220;Эффекты&#8221;:<figure id="attachment_469" style="width: 361px;" class="wp-caption aligncenter">

[<img class="size-full wp-image-469" alt="Анализируем свойства продублированных слоев" src="http://localhost:7788/third/wp-content/uploads/2013/06/disable_effects_layer.png" width="361" height="391" />][3]<figcaption class="wp-caption-text">Анализируем свойства продублированных слоев</figcaption></figure> 

Теперь уберем прозрачные пиксели фонового слоя. Для этого воспользуемся инструментов &#8220;Тримминг&#8221; (более подробно об инструменте &#8220;Тримминг&#8221; можно почитать в статье &#8220;[Photoshop &#8211; обрезка изображений (trimming)][4]&#8220;. Переходим в меню &#8220;Изображение &#8211; Тримминг&#8221;. Откроется окно настроек, в котором убедимся, что удаление лишних пикселей будет производиться на основе прозрачных пикселей и при этом обрезка будет происходить со всех сторон изображения: сверху, снизу, слева, справа. Жмем ОК:<figure id="attachment_470" style="width: 451px;" class="wp-caption aligncenter">

[<img class="size-full wp-image-470" alt="Обрезка прозрачных слоев фона" src="http://localhost:7788/third/wp-content/uploads/2013/06/trimming_pixels.png" width="451" height="235" />][5]<figcaption class="wp-caption-text">Обрезка прозрачных слоев фона</figcaption></figure> 

Видим, что фон удалился и осталось только само изображение: фон, флаг и надпись Formula. Теперь необходимо убрать фоновую заливку. Ее мы сделаем средствами CSS, в том числе и градиент. Это уменьшит размер результирующего файла, что положительно скажется на скорости загрузки сайта.

Для этого просто удалим слой Shape2, который и является фоном шапки. Выделяем его в панели слоев и жмем клавишу Delete. Получается такая картина в панели:<figure id="attachment_471" style="width: 361px;" class="wp-caption aligncenter">

[<img class="size-full wp-image-471" alt="Панель с удаленным слоем Shape2" src="http://localhost:7788/third/wp-content/uploads/2013/06/deleted_layer.png" width="361" height="269" />][6]<figcaption class="wp-caption-text">Панель с удаленным слоем Shape2</figcaption></figure> 

В рабочем окне Photoshop также изменилось кое-что. А именно &#8211; удалилась заливка и остались только значок флага и надпись Formula. Это как раз то, что нам и требовалось. И опять появилась шахматка на месте бывшего слоя Shape2. Ее мы может опять-таки, тоже удалить. А точнее &#8211; обрезать получившееся изображение тем же способом &#8211; через инструмент &#8220;Тримминг&#8221;. Ведь мы стремимся уменьшить размер результирующего изображения до минимума и лишние пиксели нам ни к чему. Обрезаем его через Тримминг и получаем в результате:<figure id="attachment_472" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-472" alt="Изображение с удаленным фоном шапки макета" src="http://localhost:7788/third/wp-content/uploads/2013/06/deleted_background-600x233.png" width="600" height="233" />][7]<figcaption class="wp-caption-text">Изображение с удаленным фоном шапки макета</figcaption></figure> 

Все готово &#8211; мы получили то, что требовалось. Осталось сохранить результирующее изображение, как и положено &#8211; для Web. Естественно, сохранение производим в формате png, так как он поддерживает прозрачные пиксели (нужные нам для фона) и хорошую передачу оттенков цветов (градиент). Сам процесс сохранения я описывать не буду &#8211; он прост и многократно был описан в Сети.

Создаем стилевые правила для шапки будущего шаблона сайта:

<pre>&lt;div class="header"&gt;
    &lt;div class="logo"&gt;
      &lt;a href="#" title="На главную"&gt;
        &lt;img src="images/logo.png"&gt;
      &lt;/a&gt;
    &lt;/div&gt;
  &lt;/div&gt;</pre>

<pre>.logo{
    position: absolute; top: 0; left: 0;
  }
  .header {
    -webkit-border-radius: 3px;
       -moz-border-radius: 3px;
            border-radius: 3px;
    -webkit-box-shadow: 0 4px 4px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255,255,255,0.3);
       -moz-box-shadow: 0 4px 4px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255,255,255,0.3);
            box-shadow: 0 4px 4px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255,255,255,0.3);
    height: 45px;
    background-color: #bf1919;
    overflow: hidden;
    position: relative;
  }</pre>

Оцените статью:  
<span id="post-ratings-465" class="post-ratings" data-nonce="ed6c84e9f0"><img id="rating_465_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(465, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_465_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(465, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_465_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(465, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_465_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(465, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_465_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(465, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_465_text"></span></span><span id="post-ratings-465-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/06/header_maket.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/06/header_layers.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/06/disable_effects_layer.png
 [4]: http://localhost:7788/third/?p=327 "Photoshop - обрезка изображений (trimming)"
 [5]: http://localhost:7788/third/wp-content/uploads/2013/06/trimming_pixels.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/06/deleted_layer.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/06/deleted_background.png