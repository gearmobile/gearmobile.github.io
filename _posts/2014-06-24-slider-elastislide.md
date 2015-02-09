---
title: Слайдер Elastislide
author: gearmobile
excerpt: Обзор слайдера Elastislide типа Carousel, созданного под библиотеку jQuery. Слайдер адаптивный, меняет свои размеры в зависимости от размера окна браузера. В качестве элементов управления применяются только кнопки перемотки вперед и назад. Кнопки генерируются скриптом Elastislide автоматически. Кроме этого, никаких других элементов управления не имеет.
layout: post
permalink: /slider-elastislide/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - 'Javascript &amp; jQuery'
tags:
  - elastslide
---
Обзор слайдера Elastislide типа Carousel, созданного под библиотеку jQuery. Слайдер адаптивный, меняет свои размеры в зависимости от размера окна браузера. В качестве элементов управления применяются только кнопки перемотки вперед и назад. Кнопки генерируются скриптом Elastislide автоматически. Кроме этого, никаких других элементов управления не имеет.

### Подключение скрипта Elastislide

Для подключения скрипта к проекту необходимо выполнить несколько шагов. Первое, нужно создать HTML-разметку:

<pre><ul id="elastic" class="elastislide-list">
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 1" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 2" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 3" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 4" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 5" /></a>
  </li>
      
</ul>
  </pre>

Обязательное условие &#8211; нужно применить к списку идентификатор (*с произвольным именем*) и класс `elastislide-list`, на который будут &#8220;вешаться&#8221; CSS-стили. А так видим, что HTML-разметка минималистская, все отлично.

Переходим на [официальную страницу Elastislide][1] и скачиваем оттуда архив с исходниками (*кнопка Download Source*).

Распаковываем архив и видим несколько папок и четыре HTML-файла с примерами работы слайдера Elastislide. Можно полюбоваться, какую красоту создает скрипт Elastislide ))

Из распакованного архива потребуются не все файлы, а только некоторые из них.

#### Подключаем JS-файлы

Из папки JS распакованного архива забираем все три js-файла и подключаем их следующим образом:

  * файл `modernizr.custom.17475.js` подключаем в head HTML-документа:

<pre></pre>

  * файлы `jquery.elastislide.js`, `jquerypp.custom.js`, `jquery-1.8.2.min.js` подключаем в теле HTML-документа, перед закрывающим тегом `</body>`:

<pre></pre>

Конечно, библиотеку jQuery можно подключать не локально, а через любой из CDN&#8217;ов &#8211; это кому как нравиться. На оф. сайте в качестве примера так и делается. jQuery используется версии 1.8.2 &#8211; я ее тоже использовал; более поздние версии не проверял на работоспособность с Elastislide.

  * там же создаем еще один js-файл, в котором инициализируем скрипт Elastislide и пропишем настройки для него (*если они понадобятся*):

<pre></pre>

#### Подключение CSS-стилей

Остался еще один файл, который нужно подключить в проект &#8211; это готовые CSS-стили &#8220;от автора&#8221;, чтобы слайдер Elastislide заработал. Забираем из папки CSS распакованного архива CSS-файл `elastislide.css` и подключаем его в head HTML-документа:

<pre><link rel="stylesheet" type="text/css" href="css/elastislide.css" />
</pre>

Остальные два файла `custom.css` и `demo.css` в папке CSS нам не нужны &#8211; они созданы автором скрипта для презентационных целей в примерах.

Итоговая картина подключения JS-скриптов, CSS-файла и HTML-разметки будет выглядеть следующим образом:

<pre>

    

<ul id="elastic" class="elastislide-list">
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 1" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 2" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 3" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 4" /></a>
  </li>
        
  
  <li>
    <a href="#"><img src="http://placehold.it/200x100" alt="Elastic 5" /></a>
  </li>
      
</ul>

    
    
    

    

<!-- Кастомный скрипт для Elastislide -->
    

  
  </pre>

Как результат успешного подключения всех файлов смотрим на картинку:<figure id="attachment_1382" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/elastislide_ready-slider-600x279.jpg" alt="Запущенный слайдер Elastislide" width="600" height="279" class="size-medium wp-image-1382" />][2]<figcaption class="wp-caption-text">Запущенный слайдер Elastislide</figcaption></figure> 

Дальше уже можно смело редактировать файл `elastislide.css` для того, чтобы &#8220;подогнать&#8221; его под текущий дизайн страницы.

На этом все.

Оцените статью:  
<span id="post-ratings-1379" class="post-ratings" data-nonce="533eb7e603"><img id="rating_1379_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1379, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1379_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1379, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1379_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1379, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1379_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1379, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1379_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1379, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_1379_text"></span></span><span id="post-ratings-1379-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://tympanus.net/codrops/2011/09/12/elastislide-responsive-carousel/ "Elastslide"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/06/elastislide_ready-slider.jpg