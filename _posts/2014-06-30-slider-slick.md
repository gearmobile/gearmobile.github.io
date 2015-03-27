---
title: Слайдер slick
author: gearmobile
excerpt: 'Обзор установки слайдера slick под библиотеку jQuery. Данный плагин занимает одно из наиболее высоких мест в рейтинге плагинов для создания слайдшоу. Наверное, это место он получил заслуженно, поэтому стоит с ним разобраться и положить в свою копилку веб-разработчика. Плагин мне понравился всем - он имеет в своем составе все функции управления, легок и прост в установке, HTML-разметка для его создания проста и семантична. В комплекте плагин slick имеет полный набор настроек, которые легко подключить в файле конфигурации.'
layout: post
permalink: /slider-slick/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 12
ratings_score:
  - 56
ratings_average:
  - 4.67
categories:
  - 'Javascript &amp; jQuery'
tags:
  - slick
---
Обзор установки слайдера slick под библиотеку jQuery. Данный плагин занимает одно из наиболее высоких мест в рейтинге плагинов для создания слайдшоу &#8211; [slick &#8211; jQuery][1]. Наверное, это место он получил заслуженно, поэтому стоит с ним разобраться и положить в свою копилочку веб-разработчика. Домашняя страничка плагина с описание установки и различных примеров работы находится здесь &#8211; [slick Demos][2]. Плагин мне понравился всем &#8211; он имеет в своем составе все функции управления, легок и прост в установке, HTML-разметка для его создания проста и семантична. В комплекте плагин slick имеет полный набор настроек, которые легко подключить в файле конфигурации.

### Подключение плагина slick

Процесс подключения плагина slick в рабочем проекте очень прост, только нужно соблюдать правильность выполнения шагов.

#### Создание разметки под slick

HTML-разметка под плагин slick семантична и проста. Достаточно создать список с произвольным именем класса. В руководстве [Getting Started][3] на официальной странице плагина slick приводится такой пример HTML-разметки:

<pre><div class="slider">
  <div>
    <img src="images/slide_02.jpg" alt="Slider 2" />
  </div>
      
  
  <div>
    <img src="images/slide_03.jpg" alt="Slider 3" />
  </div>
      
  
  <div>
    <img src="images/slide_04.jpg" alt="Slider 4" />
  </div>
      
  
  <div>
    <img src="images/slide_05.jpg" alt="Slider 5" />
  </div>
      
  
  <div>
    <img src="images/slide_06.jpg" alt="Slider 6" />
  </div>
    
</div>
  </pre>

Моя попытка создать слайдер на основе HTML-разметки в виде обычного маркированного списка:

<pre><ul>
  <li>
    <img src="images/slide_02.jpg" alt="slick 1" />
  </li>
      
  
  <li>
    <img src="images/slide_03.jpg" alt="slick 2" />
  </li>
      
  
  <li>
    <img src="images/slide_04.jpg" alt="slick 3" />
  </li>
      
  
  <li>
    <img src="images/slide_05.jpg" alt="slick 4" />
  </li>
    
</ul>
  </pre>

&#8230; успеха не принесла &#8211; плагин slick не заработал! Возможно, стоит через CSS-стили преобразовать элементы `ul`, `li` в блочные и тогда все заработает? Однако, это дополнительные действия, без которых можно обойтись и поступить так, как описано в официальной документации.

#### Получение файла плагина slick

Следующим шагом будет получение архива плагина slick. Это можно сделать несколькими способами. Первый &#8211; это скачать его со страницы [Go Get It][4]. Или же перейти на страницу GitHub автора и забрать оттуда zip-архив плагина &#8211; [slick GitHub][5]. В обоих случаях получим архив с именем `slick-master.zip`, который нужно распаковать. И разархивированной папки нам необходима только одна папка, которая находиться внутри &#8211; **slick**. Переносим ее в свой проект целиком, как есть.

#### Подключение плагина slick в HTML-документе

В &#8220;шапке&#8221; `head` HTML-документа производим подключение готовых CSS-стилей плагина slick:

<pre><link rel="stylesheet" href="slick/slick.css" />
</pre>

В теле HTML-документа перед закрывающим тегом `</body>` вставляем три строки с js-скриптами:

<pre></pre>

Как видим, в первых двух строках производится скачивание библиотеки jQuery-1.11.0 и плагина jQuery Migrate 1.2.1 через CDN. Третий плагин `slick.min.js` &#8211; сам скрипт slick, который подключается локально, из распакованной и перемещенной в проект папки **slick**.

#### Инициализация плагина slick

Перед закрывающим тегом `</body>` подключаем скрипт инициализации плагина:

<pre>$(document).ready(function(){
      $('.slider').slick({
        dots: true
      });
  });
  </pre>

Итоговая HTML-разметка и подключение CSS-таблиц, JS-скриптов будет выглядеть таким образом:

<pre>
  
  
  
    

<ul class="slider">
  <li>
    <img src="images/slide_02.jpg" alt="Slider 2" />
  </li>
        
  
  <li>
    <img src="images/slide_03.jpg" alt="Slider 3" />
  </li>
        
  
  <li>
    <img src="images/slide_04.jpg" alt="Slider 4" />
  </li>
        
  
  <li>
    <img src="images/slide_05.jpg" alt="Slider 5" />
  </li>
        
  
  <li>
    <img src="images/slide_06.jpg" alt="Slider 6" />
  </li>
      
</ul>
    
    
    
    
  
  
  </pre>

### Консоль браузера Google Chrome

Мне хочется упомянуть о такой полезной вещи, как консоль браузера Google Chrome. Почему она полезная? Потому что она уже второй раз выручает меня (первый раз это было с плагином jqFancyTransitions &#8211; [Слайдер jqFancyTransitions][6]) и помогает найти ошибки при подключении скриптов в HTML-документе. Незаменимая штука!

Чтобы проиллюстрировать пример использования и полезности консоли Chrome, запускаю в браузере индексный index.html файл, который создал ранее.

И что?! Позвольте, а где-же плагин slick &#8211; где слайдер, созданный с его помощью? Где те обещанные красоты, которые так ярко продемонстрированы на официальной странице проекта &#8211; [Demos][7]?! Странно &#8211; но их нет!

Хех, а я правильно выполнил подключение скрипта? Ну-ка, еще раз &#8220;пробегусь&#8221; по документации&#8230; Все верно, но у меня ничего не работает&#8230; Может, все-же переписать индексную страницу заново? Может быть, но таких &#8220;а может&#8221; наберется большое количество, с различными вариациями&#8230;

Но давайте я открою консоль браузера Google Chrome и перейду в ней на вкладку &#8220;Network&#8221;:<figure id="attachment_1424" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/slick_jquery_error_console-600x474.jpg" alt="Консоль браузера Google Chrome" width="600" height="474" class="size-medium wp-image-1424" />][8]<figcaption class="wp-caption-text">Консоль браузера Google Chrome</figcaption></figure> 

Вот и причина того, что плагин slick не работает на моей странице! Просто библиотеку jQuery 1.11.0 и ее плагин jQuery Migrate 1.2.1 браузеру Chrome не удалось подгрузить через CDN. Сколько бы я еще потратил времени и нервов, чтобы методом &#8220;научного тыка&#8221; определить причину &#8220;поломки&#8221;, если бы не эта консоль, неизвестно.

Разбираться, почему не удалось браузеру подгрузить оба этих файла через CDN, у меня нет ни желания, ни времени. Поэтому я просто скачаю оба этих файла &#8220;вручную&#8221; и подключу локально:

<pre></pre>

Снова запускаю индексную страницу index.html в браузере Google Chrome и &#8230; о Чудо! Плагин slick работает:<figure id="attachment_1425" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/slick_jquery_work-600x474.jpg" alt="Плагин slick работает" width="600" height="474" class="size-medium wp-image-1425" />][9]<figcaption class="wp-caption-text">Плагин slick работает</figcaption></figure> 

Картинки прокручиваются автоматически и внизу видна пагинация, сгенерированная скриптом slick согласно настройкам:

<pre>dots: true,
  autoplay: true
  </pre>

&#8230; в конфигурационном файле. Помимо этого, были сгенерированы стрелки для перемотки изображений &#8220;вручную&#8221; взад-вперед (они не видны на белом фоне HTML-страницы). Другие многочисленные настройки плагина slick можно посмотреть на официальной странице &#8211; [Settings][10].

Кстати, стоит отметить, что автор плагина slick настоятельно рекомендует выносить настройки плагина в отдельный внешний js-файл, вместо того, чтобы вставлять скрипт непосредственно в HTML-документ:

> NOTE: I highly recommend putting your initialization script in an external JS file.

В этой статье я так не поступил по одной простой причине &#8211; ради наглядности примера и быстроты его создания.

### Редактирование плагина slick

Теперь осталось дело за малым &#8211; вооружившись инспектором элементов страницы (к примеру, Firebug), &#8220;вытащим&#8221; из DOM-дерева нашей страницы имена классов нужных нам элементов и произведем их легкое редактирование через CSS-правила:

<pre>body{
    background-color: lighten(#ccc,5%);
    .slider{
      width: 300px;
      margin: 10px auto;
      padding: 5px;
      background-color: #ccc;
      border: 3px solid #000;
      @include border-radius(3px);
      .slick-dots{
        bottom: -30px;
      }
    }
  }
  </pre>

Создаю для тела HTML-документа `body` легкую заливку. Для блока со слайдером `.slider` добавлю padding, границу со скруглением и фоновую заливку; отцентрирую его на странице и немного опущу вниз. А также немного приподниму вверх блок `.slick-dots` с пагинацией.

Смотрим результат:<figure id="attachment_1426" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/slick_jquery_custom-600x474.jpg" alt="Видоизмененный слайдер slick" width="600" height="474" class="size-medium wp-image-1426" />][11]<figcaption class="wp-caption-text">Видоизмененный слайдер slick</figcaption></figure> 

### Заключение

Плагин slick мне однозначно понравился. Простая установка и подключение, генерирование элементов управления показом слайдшоу, большое количество разнообразных настроек. С разнообразными вариантами настройки внешнего вида можно и нужно разобраться на странице примеров &#8211; [Demos][7]. И подогнать под необходимые конкретные условия, если потребуется.

Удачного кодинга!

Оцените статью:  
<span id="post-ratings-1422" class="post-ratings" data-nonce="2e56a41313"><img id="rating_1422_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1422, 1, '1 Star');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1422_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1422, 2, '2 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1422_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1422, 3, '3 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1422_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1422, 4, '4 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1422_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1422, 5, '5 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>12</strong> votes, average: <strong>4,67</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1422_text"></span></span><span id="post-ratings-1422-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://plugins.jquery.com/tag/slider/ "slick"
 [2]: http://kenwheeler.github.io/slick/ "slick Demos"
 [3]: http://kenwheeler.github.io/slick/ "Getting Started"
 [4]: http://kenwheeler.github.io/slick/ "Go Get It"
 [5]: https://github.com/kenwheeler/slick/ "slick GitHub"
 [6]: http://localhost:7788/third/?p=1354 "Слайдер jqFancyTransitions"
 [7]: http://kenwheeler.github.io/slick/ "Demos"
 [8]: http://localhost:7788/third/wp-content/uploads/2014/06/slick_jquery_error_console.jpg
 [9]: http://localhost:7788/third/wp-content/uploads/2014/06/slick_jquery_work.jpg
 [10]: http://kenwheeler.github.io/slick/ "Settings"
 [11]: http://localhost:7788/third/wp-content/uploads/2014/06/slick_jquery_custom.jpg