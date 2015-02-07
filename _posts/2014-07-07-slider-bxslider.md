---
title: Слайдер bxSlider
author: gearmobile
excerpt: Обзор еще одного слайдера под библиотеку jQuery под названием bxSlider. Данный слайдер обладает полным набором возможностей, адаптивный и легко устанавливается в проекте.
layout: post
permalink: /slider-bxslider/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 10
ratings_score:
  - 43
ratings_average:
  - 4.3
categories:
  - 'Javascript &amp; jQuery'
tags:
  - bxslider
---
Обзор еще одного слайдера под библиотеку jQuery под названием bxSlider. Данный слайдер обладает полным набором возможностей, адаптивный и легко устанавливается в проекте. Адрес проживания слайдера bxSlider &#8211; [The Responsive jQuery Content Slider][1].

Конкретно какими возможностями обладает bxSlider:

  * полностью адаптивный
  * может быть горизонтальным, вертикальным
  * может содержать в себе изображения, видео или HTML-контент
  * поддержка функций touch/swipe
  * для анимаций используются CSS transitions
  * маленький размер файла, легко видоизменяется и настраивается
  * поддержка браузерами Firefox, Chrome, Safari, iOS, Android, Ie7+
  * большое число настроек

### Установка слайдера bxSlider

Установка bxSlider ничем не отличается от установки ему подобных скриптов для создания carousel. Скачиваем с сайта архив &#8211; в нем есть все необходимое для подключения и работы. Помимо этого, там есть несколько дополнительных файлов типа `jquery.easing.1.3.js` и `jquery.fitvids.js`. Но нет библиотеки jQuery, которую автор рекомендует подключать в проект через CDN. Я подключу jQuery локально, версии 1.11.1.

В HTML-файле перед закрывающим тегом body произвожу подключение скриптов в таком порядке:

<pre>...
  <!--  SCRIPTS  -->
  
  
  
  </pre>

Файл `jquery.bxslider.min.js` беру из скачанного архива, файл `bxslider.js` &#8211; произвольного имени, для настроек плагина bxSlider.

В `head` HTML-документа, помимо этого, производится подключение таблицы стилей для плагина bxSlider, которую также беру из скачанного архива. Данный шаг выполнять **совершенно необязательно** &#8211; можно обойтись без файла `jquery.bxslider.css` и тогда получим &#8220;чистый&#8221; слайдер, который можно видоизменять по своему с помощью CSS:

<pre></pre>

Плагин bxSlider подключен и готов к работе. Осталось создать HTML-разметку для него.

### HTML-разметка для слайдера bxSlider

Внутри тега `body` создаю разметку для будущего слайдера. Она проста и семантична, представляет из себя обычный маркированный список, в котором каждый элемент `li` является слайдом. Внутри `li` может размещаться изображение, видео или любой другой HTML-контент. Контейнер `ul` должен иметь класс с произвольным именем:

<pre><ul class="slider">
  <li>
    <img src="http://placehold.it/300x200" alt="bxSlider" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200" alt="bxSlider" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200" alt="bxSlider" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200" alt="bxSlider" />
  </li>
    
</ul>
  </pre>

### Инициализация скрипта bxSlider

В созданном ранее js-файле `bxslider.js` произвожу инициализацию плагина bxSlider. Важно заметить, что строка инициализации должна быть **обязательно** заключена в &#8220;обертку&#8221; `$(document).ready()`, иначе слайдер не будет работать:

<pre>$(document).ready(function(){
    $('.slider').bxSlider();
  });
  </pre>

Смотрю готовый результат:<figure id="attachment_1464" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_ready-600x317.png" alt="Запущенный слайдер bxSlider" width="600" height="317" class="size-medium wp-image-1464" />][2]<figcaption class="wp-caption-text">Запущенный слайдер bxSlider</figcaption></figure> 

Слайдер bxSlider запущен и работает &#8211; есть кнопки пагинации и перемотки, изображения крутятся при нажатии на них. Пробую отключить таблицу стилей `jquery.bxslider.css` и смотрю результат. Действительно, слайдер bxSlider получается &#8220;голым&#8221;, но рабочим:<figure id="attachment_1465" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_clean-600x317.png" alt="Чистый слайдер bxSlider" width="600" height="317" class="size-medium wp-image-1465" />][3]<figcaption class="wp-caption-text">Чистый слайдер bxSlider</figcaption></figure> 

### Стилизация слайдера bxSlider

Произведу небольшую стилизацию слайдера bxSlider. Для этого необходимо воспользоваться плагином Firebug под браузер Mozilla Firefox, чтобы инспектировать DOM-дерево и находить нужные HTML-элементы с их классами. Как можно было понять из базовой HTML-разметки, все элеметы управления слайдером генерируются скриптом автоматически.

Стилизация слайдера bxSlider с помощью CSS-правил (в данном примере это SCSS) может быть такой:

<pre>$asidePos: 50px;
  $color: #778899;

  .bx-wrapper{
    margin: 10px auto;
    width: 300px;
    border: 5px solid #fff;
    box-shadow: 0 0 5px #ccc;
    position: relative;
    .bx-viewport{
      box-shadow: 0 0 5px #ccc;
    }
    /*  Скрывать пагинацию  */
    .bx-pager{
      display: none;
    }
    /*  Кнопки перемотки  */
    .bx-prev,
    .bx-next{
      position: absolute;
      top: 92px;
      width: 20px;
      height: 20px;
      background-color: $color;
      @include squish-text;
      @include border-radius(50%);
      @include single-transition(background-color, .1s, ease-in-out);
      &#038;:hover,&#038;:focus{
        outline: none;
        background-color: darken($color,5%);
      }
      &#038;:active{
        background-color: darken($color,10%);
      }
    }
    .bx-prev{
      left: -$asidePos;
    }
    .bx-next{
      right: -$asidePos;
    }
    img{
      vertical-align: top;
    }
  }
  </pre>

И посмотрим результат наших трудов. Уже гораздо лучше, однако:<figure id="attachment_1466" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_styled-600x326.png" alt="Стилизованный слайдер bxSlider" width="600" height="326" class="size-medium wp-image-1466" />][4]<figcaption class="wp-caption-text">Стилизованный слайдер bxSlider</figcaption></figure> 

### Настройка слайдера bxSlider

Плагин bxSlider имеет большое количество настроек, которые легко подключать в коде. Разнообразные (и многочисленные) примеры создания слайдера приведены на странице &#8211; [Examples][5]. Эти примеры **можно и стоит изучить** (*хотя бы слегка, для будущего*).

В этой статье давайте я воссоздам один из приведенных на странице [Examples][5] примеров. Пусть это будет слайдер с автоматической прокруткой и кнопками управления прокруткой &#8211; запуско и остановкой. Такой готовый пример размещен здесь &#8211; [Auto show with start / stop controls][6]. Я просто сделаю свой собственный дубликат, со своими стилями.

Для этого в SCSS-коде добавляю такие строки:

<pre>/*  auto controls  */
  .bx-controls-auto{
    margin: 5px 0 0;
    @include pie-clearfix;
    .bx-controls-auto-item{
      display: inline-block;
      float: left;
      .bx-start,
      .bx-stop{
        display: block;
        @include squish-text;
        @include single-transition(background-color, .1s, ease-in-out);
      }
      .bx-start{
        @include arrow-right(7px,lighten($color,20%));
      }
      .bx-stop{
        width: 14px;
        height: 14px;
        margin: 0 0 0 5px;
        background-color: lighten($color,20%);
      }
    }
  }
  </pre>

HTML-разметку на странице я не меняю, как вы могли заметить. Блок `.bx-controls-auto` генерируется скриптом bxSlider автоматически.

Файл настроек `bxslider.js` подправляю, чтобы он выглядел таким образом:

<pre>$(document).ready(function(){
    $('.slider').bxSlider({
      auto: true,
      autoControls: true
    });
  });
  </pre>

Смотрю результат в браузере:<figure id="attachment_1467" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_autoplay-600x326.png" alt="Слайдер bxSlider с автоматической прокруткой" width="600" height="326" class="size-medium wp-image-1467" />][7]<figcaption class="wp-caption-text">Слайдер bxSlider с автоматической прокруткой</figcaption></figure> 

Отлично! Появились кнопки запуска и остановки показа слайдшоу; сам слайдер стартует автоматически, при открытии страницы в окне браузера.

### Заключение

Плагин bxSlider мне однозначно понравился. Семнатичная простая разметка, использование произвольного имени класса (а не идентификатора), автоматическое генерирование HTML-элементов слайдера, большое количество настроек, хорошие эффекты, простота подключения.

Все эти преимущества однозначно сделали плагин bxSlider номером один в моей копилке.

Оцените статью:  
<span id="post-ratings-1461" class="post-ratings" data-nonce="14b2509690"><img id="rating_1461_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1461, 1, '1 Star');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1461_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1461, 2, '2 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1461_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1461, 3, '3 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1461_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1461, 4, '4 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1461_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1461, 5, '5 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>10</strong> votes, average: <strong>4,30</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1461_text"></span></span><span id="post-ratings-1461-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://bxslider.com/ "The Responsive jQuery Content Slider"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_ready.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_clean.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_styled.png
 [5]: http://bxslider.com/examples "Examples"
 [6]: http://bxslider.com/examples/auto-show-start-stop-controls "Auto show with start / stop controls"
 [7]: http://localhost:7788/third/wp-content/uploads/2014/07/bxslider_autoplay.png