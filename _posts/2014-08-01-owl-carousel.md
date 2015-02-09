---
title: Слайдер Owl Carousel
author: gearmobile
excerpt: 'Встретил на Google+ упоминание о плагине под jQuery для создания карусели - OWL Carousel. Попробовал с ним разобраться и посмотреть примеры создания слайдеров на официальной странице. Могу сказать, что я впечатлен данным скриптом и его возможностями. Слайдер адаптивный, имеет множество настроек, обладает хорошими эффектами "из коробки". Мое личное мнение - отличный выбор для применения на практике!'
layout: post
permalink: /owl-carousel/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 17
ratings_average:
  - 4.25
categories:
  - 'Javascript &amp; jQuery'
tags:
  - owlcarousel
---
Встретил на Google+ упоминание о плагине под jQuery для создания карусели &#8211; OWL Carousel. Попробовал с ним разобраться и посмотреть примеры создания слайдеров на официальной странице. Могу сказать, что я впечатлен данным скриптом и его возможностями. Слайдер адаптивный, имеет множество настроек, обладает хорошими эффектами &#8220;из коробки&#8221;. Мое личное мнение &#8211; отличный выбор для применения на практике!

Официальная страница проекта располагается здесь &#8211; [OWL Carousel][1]. Стабильная версия скрипта на данный момент &#8211; v1.3.2, но на странице упоминается о версии 2.0.0-beta. Для своей работы плагин требует библиотеки jQuery версии не ниже 1.7.

Ниже я попробую создать простой вариант карусели с помощью плагина OWL Carousel. Более интересные и продвинутые варианты, я думаю, показывать не имеет смысла. По той простой причине, что разобравшись с базовым вариантом, всегда можно его улучшить. И для этой цели как ничто лучше подойдут примеры на официальной странице &#8211; [Demo][2] и [More Demo][3]. Стоит сказать, что для себя я увидел там готовые решения практически на все случаи жизни.

### Подключение OWL Carousel

Для подключения плагина OWL Carousel к готовому проекту необходимо получить архив плагина с официальной страницы &#8211; [OWL Carousel][1] или с GitHub &#8211; [OwlCarousel][4]. В архиве имеется все, что необходимо &#8211; библиотека jQuery, плагин owl.carousel.min.js, готовые CSS-стили для карусели. Ничего сложного или необычного в подключении плагина OWL Carousel нет &#8211; все стандартно.

HTML-разметка и подключение скрипта будут выглядеть следующим образом:

<pre>

    

<ul id="carousel" class="owl-carousel carousel">
  <li>
    <img src="images/owl1.jpg" width="300" height="200" alt="Owl_1" />
  </li>
        
  
  <li>
    <img src="images/owl2.jpg" width="300" height="200" alt="Owl_2" />
  </li>
        
  
  <li>
    <img src="images/owl3.jpg" width="300" height="200" alt="Owl_3" />
  </li>
        
  
  <li>
    <img src="images/owl4.jpg" width="300" height="200" alt="Owl_4" />
  </li>
        
  
  <li>
    <img src="images/owl5.jpg" width="300" height="200" alt="Owl_5" />
  </li>
        
  
  <li>
    <img src="images/owl6.jpg" width="300" height="200" alt="Owl_6" />
  </li>
        
  
  <li>
    <img src="images/owl7.jpg" width="300" height="200" alt="Owl_7" />
  </li>
        
  
  <li>
    <img src="images/owl8.jpg" width="300" height="200" alt="Owl_8" />
  </li>
      
</ul>


    

<!--  SCRIPTS  -->
    
    
    
  
  </pre>

В `head` подключаются две готовых CSS-таблицы из архива &#8211; `owl.carousel.css` и `owl.theme.css`. Таблица `style.css` &#8211; опциональная, для настройки плагина под конкретные условия.

Тип HTML-элементов для создания разметки слайдера, по большому счету, не имеет особого значения, так как скрипт OWL Carousel умеет работать со всеми типами. Главное, чтобы у блока-обертки имелся обязательный класс `owl-carousel`, к которому будет производиться привязка стилей из файла `owl.carousel.css`.

В конце тела `body` документа подключаются библиотека jQuery, скрипт плагина OWL Carousel и файл настроек данного скрипта.

Базовая конфигурация js-файла `settings.js` выглядит следующим образом:

<pre>$(document).ready(function() {
    $("#carousel").owlCarousel();
  });
  </pre>

Все, можно смотреть на готовый (*слегка подредактированный*) результат:<figure id="attachment_1579" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/owl_carousel-base-600x410.jpg" alt="Базовый вариант слайдера OWL Carousel" width="600" height="410" class="size-medium wp-image-1579" />][5]<figcaption class="wp-caption-text">Базовый вариант слайдера OWL Carousel</figcaption></figure> 

### Настройка плагина OWL Carousel

Скрипт OWL Carousel имеет большое количество настроек, которые добавляются или убираются в файле настроек. Ссылка на страницу с полным списком настроек располагается здесь &#8211; [Customizing OWL Carousel][6].

К примеру, переменная `items` задает количество одновременно показываемых в слайдере изображений:

<pre>items: 5
  </pre>

Переменные `itemsDesktopSmall`, `itemsTablet`, `itemsTabletSmall`, `itemsMobile` устанавливают количество одновременно отображаемых изображений в зависимости от размера окна браузера. Например, запись вида `itemsDesktop: [1199,4]` &#8220;говорит&#8221; браузеру, что при размере окна **меньше или равному** 1199px следует отображать одновременно только четыре изображения:

<pre>itemsDesktop: [1199,4]
  </pre>

Переменная `singleItem` устанавливает, отображать ли только одно изображение в слайдере или несколько:

<pre>singleItem: false
  </pre>

Переменные `navigation` и `pagination` управляют возможностью включения или выключения навигации\пагинации у слайдера:

<pre>navigation: true,
  pagination: true
  </pre>

Автоматическая прокрутка изображений в слайдере включается с помощью переменной `autoPlay`:

<pre>autoPlay: true
  </pre>

Имеются множество других настроек плагина OWL Carousel, с которыми можно легко разобраться на официальной странице. Все перечислять здесь я не буду.

### Варианты слайдера OWL Carousel

Стоит &#8220;побродить&#8221; по странице с демонстрационными примерами работы плагина OWL Carousel. Там есть на что посмотреть и что подобрать для себя.

Мне понравились примеры создания слайдеров &#8211; [Lazy Load][7] и [Auto Height][8].

Наиболее интересные (*для меня*) примеры расположены в списке со ссылками.

К примеру, по ссылке [CSS3 Transitions][9] располагается образец слайдера с эффектом перехода, основанном на CSS3-свойстве transition. Более того, из выпадающего списка можно прямо на странице подобрать себе подходящий эффект &#8211; своеобразный конструктор получается:<figure id="attachment_1578" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/owl_carousel-transitions-600x453.jpg" alt="Слайдер OWL Carousel с эффектом transition" width="600" height="453" class="size-medium wp-image-1578" />][10]<figcaption class="wp-caption-text">Слайдер OWL Carousel с эффектом transition</figcaption></figure> 

Или пример создания слайдера с расположенной вверху полосой progress bar &#8211; [Progress Bar][11].

### Заключение

Плагин OWL Carousel мне понравился и я буду стараться применять его на практике, при верстке страниц.

Оцените статью:  
<span id="post-ratings-1577" class="post-ratings" data-nonce="ec34cba003"><img id="rating_1577_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1577, 1, '1 Star');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1577_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1577, 2, '2 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1577_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1577, 3, '3 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1577_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1577, 4, '4 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1577_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1577, 5, '5 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>4,25</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1577_text"></span></span><span id="post-ratings-1577-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://owlgraphic.com/owlcarousel/ "OWL Carousel"
 [2]: http://owlgraphic.com/owlcarousel/#demo "Demo"
 [3]: http://owlgraphic.com/owlcarousel/#more-demos "More Demo"
 [4]: https://github.com/OwlFonk/OwlCarousel "OwlCarousel"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/08/owl_carousel-base.jpg
 [6]: http://owlgraphic.com/owlcarousel/#customizing "Customizing OWL Carousel"
 [7]: http://owlgraphic.com/owlcarousel/demos/lazyLoad.html "Lazy Load"
 [8]: file:///media/aaron/small_flash/source/owl.carousel/demos/autoHeight.html "Auto Height"
 [9]: file:///media/aaron/small_flash/source/owl.carousel/demos/transitions.html "CSS3 Transitions"
 [10]: http://localhost:7788/third/wp-content/uploads/2014/08/owl_carousel-transitions.jpg
 [11]: http://owlgraphic.com/owlcarousel/demos/progressBar.html "Progress Bar"