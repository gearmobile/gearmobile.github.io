---
title: 'Photoshop &#8211; как определить альфа-канал слоя'
author: gearmobile
layout: post
permalink: /photoshop-%d0%ba%d0%b0%d0%ba-%d0%be%d0%bf%d1%80%d0%b5%d0%b4%d0%b5%d0%bb%d0%b8%d1%82%d1%8c-%d0%b0%d0%bb%d1%8c%d1%84%d0%b0-%d0%ba%d0%b0%d0%bd%d0%b0%d0%bb-%d1%81%d0%bb%d0%be%d1%8f/
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
Недавно столкнулся с такой проблемой. Точнее &#8211; проблемой ее можно назвать с большой натяжкой. Для новичка в Photoshop это и может быть трудностью, но не для опытного пользователя. Итак, в чем же заключается та трудность, с которой мне пришлось иметь дело?

Имеется макет сайта в формате PSD. В нем есть несколько фоновых слоев &#8211; один основной, второй для контентной части. Для наглядности приведу примеры обоих слоев:<figure id="attachment_322" style="width: 433px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/backgrounds.png" alt="Два фоновых слоя макета в Photoshop" width="433" height="296" class="size-full wp-image-322" />][1]<figcaption class="wp-caption-text">Два фоновых слоя макета в Photoshop</figcaption></figure> 

Если с получением основного фона нет каких-либо проблем &#8211; достаточно выделить его и сохранить отдельным изображением (сохранять придется целиком, так как у него нет повторяющихся частей). То со вторым фоном будут некоторые трудности (по крайней мере, у меня).

Выделяем фон контентной части. Видим, что из себя он представляет фоновую заливку. Градиент при ее создании не использовался. Из эффектов имеются только внутренняя тень и внешняя тень, которые мы отключим. Обе тени легко воссоздать с помощью стилевых правил CSS:<figure id="attachment_323" style="width: 357px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/contentbackground-effects.png" alt="Эффекты контентного фона в Photoshop" width="357" height="221" class="size-full wp-image-323" />][2]<figcaption class="wp-caption-text">Эффекты контентного фона в Photoshop</figcaption></figure> 

И приведу изображение самого фона контентной части, представленного одним слоем, продублированным в новый документ:<figure id="attachment_324" style="width: 381px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/contentbackground.png" alt="Фоновый слой контентной части в Photoshop" width="381" height="296" class="size-full wp-image-324" />][3]<figcaption class="wp-caption-text">Фоновый слой контентной части в Photoshop</figcaption></figure> 

Внимательно смотрим на скриншот и видим. Что мы видим? Слой с заливкой однотонной, в которой градиент не применяется. Вырезать кусок изображения, чтобы использовать его в качестве фонового изображения контентной части нет смысла. Более правильным решением будет использовать цвет изображения через свойство background. Однако, даже &#8220;на глаз&#8221; видно, что фон имеет прозрачность, которую мы также должны передать через стилевые правила CSS.

Как же узнать значение прозрачности слоя? Не скрою, для меня до данного момента это было загадкой. Но все решилось очень просто. Открываем свойства слоя Shape13 двойным щелчком на нем. В появившемся окне свойств видим такую картину:<figure id="attachment_325" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/contentbackground-alphachannel-600x305.png" alt="Свойства фоновой заливки в Photoshop" width="600" height="305" class="size-medium wp-image-325" />][4]<figcaption class="wp-caption-text">Свойства фоновой заливки в Photoshop</figcaption></figure> 

Смотрим в подраздел &#8220;Дополнительные параметры&#8221; в правой части. В этом подразделе находим параметр (самый верхний) &#8220;Непрозрачность заливки&#8221;. И видим значение этого параметра &#8211; 45%. Это и есть прозрачность фоновой заливки контентной части.

Теперь осталось написать CSS-правила для этого слоя:

<pre>.content {
  background:#2b2e28;
  background:rgba(43, 46, 40, .45);
}</pre>

В первом правиле background: #2b2e28 мы обошлись значением цвета в формате HEX, который не поддерживает передачу полупрозрачности. Это сделано для браузеров, которые не могут передать полупрозрачность фонового слоя и вообще не понимают такого свойства, как полупрозрачность.

Во втором случае background: rgba(43, 46, 40, .45) цвет задан через значение rgba, где a &#8211; это альфа-канал. Второе правило было создано для современных браузеров, которые &#8220;понимают&#8221;, что такое полупрозрачность и могут ее передать через соответствующие CSS-правила. Значение альфа-канала, как мы узнали в Photoshop, равно 45%. Поэтому в правилах CSS значение 45% прописываем так &#8211; .45. Значение каналов rgb также узнаем в Photoshop (в том же окне, в котором мы брали значение HEX) и прописываем в соответствии с синтаксисом &#8211; 43, 46, 40.

Оцените статью:  
<span id="post-ratings-321" class="post-ratings" data-nonce="851e87f234"><img id="rating_321_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(321, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_321_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(321, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_321_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(321, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_321_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(321, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_321_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(321, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_321_text"></span></span><span id="post-ratings-321-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/backgrounds.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/contentbackground-effects.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/contentbackground.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/contentbackground-alphachannel.png