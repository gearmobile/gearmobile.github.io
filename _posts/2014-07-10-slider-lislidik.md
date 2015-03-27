---
title: Слайдер liSlidik
author: gearmobile
excerpt: 'На моем пути повстречался еще один плагин для создания карусели (carousel), основанный на библиотеке jQuery. Имя этого плагина запоминающиеся - liSlidik. Насколько я правильно понял, этот плагин был создан одним или несколькими русскоязычными веб-разработчиками.'
layout: post
permalink: /slider-lislidik/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - 'Javascript &amp; jQuery'
tags:
  - jquery
  - lislidik
---
На моем пути повстречался еще один плагин для создания карусели (carousel), основанный на библиотеке jQuery. Имя этого плагина запоминающиеся &#8211; liSlidik и проживает он здесь &#8211; [liSlidik &#8211; jQuery Responsive Slider][1]. Насколько я правильно понял, этот плагин был создан одним или несколькими русскоязычными веб-разработчиками. В принципе, вся документация с примерами подробно расписана на русском языке на этой странице и нет нужды пересказывать уже сказанное. Однако, я хотел разобраться с плагином liSlidik &#8211; понять, как его подключать, настраивать и управлять. Поэтому все же появился обзор этого слайдера, который будет представлен ниже.

Сразу скажу, что плагин liSlidik мне **не понравился**. На это есть несколько причин, которые я укажу ниже, в самом обзоре. Причины эти могут быть субъективными, но все же они повлияли на мой вывод.

### Установка плагина liSlidik

Установка и подключение плагина liSlidik производится совершенно стандартно для скриптов подобного рода. Сначала подключается библиотека jQuery (в этом обзоре использовалась версия 1.8), затем подключается сам скрипт liSlidik, а в конце &#8211; js-файл с инициализацией скрипта и его настройками:

<pre>...
    <!--  SCRIPTS  -->
    
    
    
  &lt;/body>
  </pre>

Скачать архив скрипта liSlidik можно с домашней страницы проекта по это ссылке &#8211; [liSlidik Download][2]. Помимо этого, на jsFiddle выложен исходный код скрипта с примерами создания разных вариантов слайдов &#8211; [liSlidik Demo][3]. Библиотеку jQuery можно подключить через CDN или скачать для локального подключения &#8211; это кому как нравиться.

### HTML-разметка для liSlidik

Разметка в HTML-документе для будущего слайдера под управлением скрипта liSlidik проста и семантична &#8211; в этом плане все на уровне современной веб-разработки. Структура будущего слайдера представляет из себя обычный маркированный список с вложенными изображениями:

<pre><ul id="slider" class="slider">
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 1" alt="liSlidik 0" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 2" alt="liSlidik 1" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 3" alt="liSlidik 2" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 4" alt="liSlidik 3" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 5" alt="liSlidik 4" />
  </li>
    
</ul>
  </pre>

Единственный важный момент при создании HTML-разметки заключается в том, что для элемента `ul` необходимо **задать идентификатор**, к которому будет &#8220;цепляться&#8221; скрипт liSlidik &#8211; **иначе слайдер не заработает** (*мне этот факт не понравился, так как я не люблю идентификаторы и стараюсь всячески избегать их использования*). Класс для элемента `ul` понадобиться для последующей стилизации слайдера на HTML-странице.

### Инициализация скрипта liSlidik

Для &#8220;запуска&#8221; скрипта liSlidik нужно его **инициализировать**, создав простой js-файл и прописав в нем такие строки:

<pre>$(document).ready(function(){
    $('#slider').liSlidik();
  });
  </pre>

### Минимальная стилизация скрипта liSlidik

Слайдер liSlidik после всех выполненных выше мною шагов **не заработает**, на самом деле. Потому что для его работы необходима **минимальная CSS-стилизация**, которую я выполню ниже. Стоит ли говорить, что данный шаг я бы не смог выполнить без незаменимого плагина Firebug под Mozilla Firefox?!

Минимальная CSS-стилизация слайдера liSlidik:

<pre>.slider{
    width: 300px;
    height: 200px;
    margin: 20px auto;
    position: relative;
    li{
      position: absolute;
      top: 0;
      left: 0;
      img{
        vertical-align: top;
      }
    }
  </pre>

Конечно, можно воспользоваться готовыми CSS-стилями из архива скрипта liSlidik; но зачем пользоваться чужим кодом, когда можно создать более чистый и маленький по размеру свой собственный код, мне не понятно. Конечно, в приведенном выше коде значения свойств `width` и `height` являются произвольными и зависят от конкретных условий &#8211; ставить нужно вместо них то, что необходимо. Это же относится и к `margin: 20px auto;`, которое было применено здесь для &#8220;красоты&#8221;.

Вот теперь слайдер liSlidik готов к работе. Более того &#8211; он работает! Это минималистичный слайдер, без каких-либо кнопок управления:<figure id="attachment_1473" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_clean-600x451.png" alt="Скрипт liSlidik работает" width="600" height="451" class="size-medium wp-image-1473" />][4]<figcaption class="wp-caption-text">Скрипт liSlidik работает</figcaption></figure> 

### Кнопки управления для liSlidik

Скрипт liSlidik имеет в своем составе полный набор органов управления создаваемым им слайдером. Начну с малого и приступлю к созданию кнопок перемотки взад-вперед для слайдшоу. Стоит сразу сказать, что все органы управления показом слайдшоу в скрипте liSlidik **не создаются автоматически &#8211; их нужно создавать вручную** (*данный факт мне также не совсем понравился*):

<pre><!--  arrows  -->
  

<a data-slidik="slider" class="next" href="#">Next</a>
  <a data-slidik="slider" class="prev" href="#">Prev</a>
  </pre>

HTML-разметка для кнопок перемотки создается через элемент `a`, у которого обязательным атрибутом должен быть `data-slidik="slider"`, где `slider` &#8211; это имя идентификатора нашего слайдера. Классы `class="next"` и `class="prev"` присутствуют для тех же целей, что и в элементе `ul` &#8211; на них &#8220;вешаются&#8221; CSS-стили:

<pre>/*  ARROWS  */
  .next,
  .prev{
    display: block;
    width: 20px;
    height: 20px;
    position: absolute;
    z-index: 2;
    top: 95px;
    background-color: #000;
    @include border-radius(50%);
    @include squish-text;
    @include single-transition(background-color, .2s, ease-in);
  }
  .next{
    left: 10px;
    &#038;:hover,&#038;:focus{
      background-color: lighten(#000,20%);
    }
  }
  .prev{
    right: 10px;
    &#038;:hover,&#038;:focus{
      background-color: lighten(#000,20%);
    }
  }
  </pre>

Смотрим результат подключения кнопок перемотки в liSlidik:<figure id="attachment_1474" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_arrows-600x451.png" alt="Плагин liSlidik c кнопками перемотки" width="600" height="451" class="size-medium wp-image-1474" />][5]<figcaption class="wp-caption-text">Плагин liSlidik c кнопками перемотки</figcaption></figure> 

### Пагинация в слайдере liSlidik

Подключение пагинации в скрипте liSlidik выполняется аналогично &#8211; нужно вручную создать блочный элемент `div` с атрибутом `data-slidik="slider"` и классом `class="dotted"` (**который также обязателен в данном случае!**):

<pre><!--  pagination  -->
  

<div data-slidik="slider" class="dotted">
  
</div>
  </pre>

Создаю для нового элемента CSS-стили. Снова оговорюсь, что для блока пагинации (*насколько я правильно понял*) имя класса `dotted` является обязательным. Я пробовал менять это имя на произвольное и в результате слайдер перестал работать (*вот такие мелкие обязательства мне и не нравятся в этом плагине!*):

<pre>/*  PAGINATION  */
  .dotted{
    position: absolute;
    bottom: 2px;
    left: 2px;
    z-index: 3;
    @include pie-clearfix;
    .dottedItem{
      cursor: pointer;
      float: left;
      margin: 0 5px;
      width: 20px;
      height: 20px;
      line-height: 20px;
      color: #fff;
      font-size: 12px;
      background-color: lighten(#000,30%);
      text-align: center;
      @include border-radius(50%);
      @include single-transition(background-color, .2s, ease-in);
      &#038;:hover,&#038;:focus{
        background-color: lighten(#000,40%);
      }
      &#038;.cur{
        background-color: lighten(#000,50%);
      }
    }
  }
  </pre>

Присутствующее в коде выше имя класса `.cur` обозначает активный элемент, который можно стилизовать на свой выбор. Еще один странный момент, связанный со слайдером liSlidik &#8211; внимательно посмотрите на снимок работающего скрипта:<figure id="attachment_1475" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_pagination-600x451.png" alt="Скрипт liSlidik c пагинацией" width="600" height="451" class="size-medium wp-image-1475" />][6]<figcaption class="wp-caption-text">Скрипт liSlidik c пагинацией</figcaption></figure> 

Ничего не замечаете? Нумерация в данной пагинации начинается с нуля! )) Это весьма странный факт, ибо обычные посетители сайта не являются программистами и для них нумерация с нуля, мягко выражаясь, непривычна и необычна.

### Заголовок слайдера liSlidik

Заголовок для слайдера liSlidik создается вручную (*неужели нельзя создать скрипт, который автоматически генерирует нужные HTML-элементы?*) также с помощью блочного элемента `div`, для которого прописывается атрибут `data-slidik="slider"` с обязательным именем класса `class="caption"`:

<pre><!--  caption  -->
      

<div data-slidik="slider" class="caption">
  
</div>
  </pre>

И произвольные CSS-стили для него:

<pre>/*  CAPTION  */
  .caption{
    position: absolute;
    top: 0;
    left: 0;
    z-index: 4;
    padding: 6px 0;
    text-indent: 1em;
    width: 100%;
    background-color: rgba(0,0,0,.6);
    color: rgba(255,255,255,.5);
  }
  </pre>

Текст для показа на странице скрипт liSlidik берет из содержимого атрибута `alt=` для элемента `img`. Поэтому не забудьте его прописать в своей HTML-разметке!<figure id="attachment_1476" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_caption-600x451.png" alt="Скрипт liSlidik c заголовком" width="600" height="451" class="size-medium wp-image-1476" />][7]<figcaption class="wp-caption-text">Скрипт liSlidik c заголовком</figcaption></figure> 

### Миниатюры в скрипте liSlidik

Плагин liSlidik имеет возможность создания миниатюр в виде галлереи изображений, которая выступает в роли пагинации. На странице демо-примеров показан вариант такого слайдшоу. Однако, у меня не было желания разбираться с вопросом построения thumnnails в этом примере.

### Заключение

Все примеры и варианты создания слайдеров под управлением скрипта liSlidik можно посмотреть на официальной страничке проекта &#8211; [liSlidik &#8211; jQuery Responsive Slider][1]. Ниже привожу полный HTML и SCSS-код примера, рассмотренного в данной статье:

HTML:

<pre><ul id="slider" class="slider">
  <li class="show">
    <img src="http://placehold.it/300x200&#038;text=liSlidik 1" alt="liSlidik 0" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 2" alt="liSlidik 1" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 3" alt="liSlidik 2" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 4" alt="liSlidik 3" />
  </li>
      
  
  <li>
    <img src="http://placehold.it/300x200&#038;text=liSlidik 5" alt="liSlidik 4" />
  </li>
      
  <!--  arrows  -->
      
  
  <a data-slidik="slider" class="next" href="#">Next</a>
      <a data-slidik="slider" class="prev" href="#">Prev</a>
      <!--  pagination  -->
      
  
  <div data-slidik="slider" class="dotted">
    
  </div>
      
  
  <!--  caption  -->
      
  
  <div data-slidik="slider" class="caption">
    
  </div>
      
  
  <!--  previews  -->
      
  
  <!-- <div data-slidik="slider" class="thumbs"></div> -->
    
</ul>

  

<!--  SCRIPTS  -->
  
  
  
  </pre>

SCSS:

<pre>.slider{
    width: 300px;
    height: 200px;
    margin: 20px auto;
    position: relative;
    li{
      border: 2px solid #000;
      position: absolute;
      top: -2px;
      left: -2px;
      &#038;.show{
        display: block;
        z-index: 2;
      }
      img{
        vertical-align: top;
      }
    }
    /*  ARROWS  */
    .next,
    .prev{
      display: block;
      width: 20px;
      height: 20px;
      position: absolute;
      z-index: 2;
      top: 95px;
      background-color: #000;
      @include border-radius(50%);
      @include squish-text;
      @include single-transition(background-color, .2s, ease-in);
    }
    .next{
      left: 10px;
      &#038;:hover,&#038;:focus{
        background-color: lighten(#000,20%);
      }
    }
    .prev{
      right: 10px;
      &#038;:hover,&#038;:focus{
        background-color: lighten(#000,20%);
      }
    }
    /*  PAGINATION  */
    .dotted{
      position: absolute;
      bottom: 2px;
      left: 2px;
      z-index: 3;
      @include pie-clearfix;
      .dottedItem{
        cursor: pointer;
        float: left;
        margin: 0 5px;
        width: 20px;
        height: 20px;
        line-height: 20px;
        color: #fff;
        font-size: 12px;
        background-color: lighten(#000,30%);
        text-align: center;
        @include border-radius(50%);
        @include single-transition(background-color, .2s, ease-in);
        &#038;:hover,&#038;:focus{
          background-color: lighten(#000,40%);
        }
        &#038;.cur{
          background-color: lighten(#000,50%);
        }
      }
    }
    /*  CAPTION  */
    .caption{
      position: absolute;
      top: 0;
      left: 0;
      z-index: 4;
      padding: 6px 0;
      text-indent: 1em;
      width: 100%;
      background-color: rgba(0,0,0,.6);
      color: rgba(255,255,255,.5);
    }
  }
  </pre>

Оцените статью:  
<span id="post-ratings-1471" class="post-ratings" data-nonce="6ef550ef0e"><img id="rating_1471_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1471, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1471_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1471, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1471_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1471, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1471_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1471, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1471_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1471, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1471_text"></span></span><span id="post-ratings-1471-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://masscode.ru/index.php/k2/item/46-lislidik "liSlidik - jQuery Responsive Slider"
 [2]: http://masscode.ru/files/zip/liSlidik.zip "liSlidik Download"
 [3]: http://jsfiddle.net/yurik417/R5jB6/8/ "liSlidik Demo"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_clean.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_arrows.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_pagination.png
 [7]: http://localhost:7788/third/wp-content/uploads/2014/07/lislidik_caption.png