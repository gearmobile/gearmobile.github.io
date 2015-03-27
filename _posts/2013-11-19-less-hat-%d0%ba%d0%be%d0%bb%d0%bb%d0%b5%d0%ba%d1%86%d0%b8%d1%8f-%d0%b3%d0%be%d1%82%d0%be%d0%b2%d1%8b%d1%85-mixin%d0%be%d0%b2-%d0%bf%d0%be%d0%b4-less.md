---
title: 'LESS Hat &#8211; коллекция готовых mixin&#8217;ов под LESS'
author: gearmobile
layout: post
permalink: /less-hat-%d0%ba%d0%be%d0%bb%d0%bb%d0%b5%d0%ba%d1%86%d0%b8%d1%8f-%d0%b3%d0%be%d1%82%d0%be%d0%b2%d1%8b%d1%85-mixin%d0%be%d0%b2-%d0%bf%d0%be%d0%b4-less/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 16
ratings_average:
  - 4
categories:
  - Статьи по CSS
tags:
  - LESS Hat
---
Продолжение темы препроцессоров для CSS, которая для меня намного интереснее всех остальных. На этот раз остановимся на препроцессоре LESS, ибо было бы странно рассказать о SASS (SCSS) и не упомянуть о не менее популярном его аналоге. Преимуществ у LESS столько же, сколько и недостатков.

Эта статья является моей попыткой на личном опыте познакомиться с LESS Hat и сравнить ее с Compass. Про сам LESS и его синтаксис я рассказывать не буду &#8211; это глупо, ибо документация для этого препроцессора прекрасно оформлена и переведена на русский язык на оф. сайте проекта.

Плюсы &#8211; этот препроцессор развивается более динамично, это более молодой проект. Синтаксис LESS интуитивно понятный и максимально приближен к CSS, поэтому новички могут освоить его совсем без труда. Документация для LESS гораздо более подробная, с примерами и переведена на множество языков, что облегчает его изучение (для SASS это серьезный недостаток, я сам с этим сталкиваюсь постоянно, когда изучаю Compass). Ну и последний немаловажный момент, который оказывает существенное влияние на распространенность LESS, это тот факт, что он включен в состав модного и известного фреймворка Bootstrap. То есть, все компоненты этого фреймворка созданы с использованием данного препроцессора. А если учесть, что один из трех китов CMS &#8211; Joomla 3 &#8211; создана на Bootstrap, то можно только гадать, куда заведет этот процесс.

К недостаткам LESS лично я могу отнести такой факт, как большое время для компиляции (хотя на оф. сайте один из создателей Bootstrap отвечал на вопрос, что им выбран препроцессор LESS как раз из-за высокой скорости компиляции, ибо он написан на языке Javascript). Еще один момент в минус LESS &#8211; файл с расширением .less компилируется каждый раз при обращении к нему браузера. В SASS производится создание файла .css из .scss &#8220;раз и навсегда&#8221;, там не нужно что-то собирать на лету, а он уже готовый подключается в HTML-документ. И последнее &#8211; LESS не имеет на сегодня такой продвинутой библиотеки миксинов, как Compass для SASS (SCSS). Точнее &#8211; подобная библиотека уже есть и ее название LESS Hat (глупо было бы, если бы такая библиотека не появилась). Однако она уступает по своим возможностям Compass.

Итак, мы уже выяснили, что LESS Hat &#8211; аналог Compass под SASS (SCSS). Если кто незнаком с последним, то можно прочитать краткий обзор в этой статье &#8211; &#8220;[Compass &#8211; фреймворк под SASS (SCSS)][1]&#8220;. Библиотека LESS Hat была создана командой, которая разработала плагин под Adobe Photoshop с названием CSS Hat (www.csshat.com). Этот плагин выполняет автоматизированные операции по переводу свойств любого элемента на psd-макете в свойства CSS. То есть, он старается упростить и ускорить задачу верстальщика, которую тот обычно выполняет вручную. Плагин CSS Hat не бесплатный, цену его я не знаю (это нетрудно узнать) и сам им не пользовался ни разу, поэтому ничего не могу сказать по этому поводу.

Проект LESS Hat живет здесь &#8211; (http://lesshat.com) и на сегодняшний момент является самой большой и популярной библиотекой готовых миксинов под препроцессор LESS. В отличие от плагина CSS Hat, библиотека LESS Hat бесплатная для использования. На момент написания статьи самая свежая версия этой библиотеки &#8211; v2.0.7, которую я и забираю со страницы проекта для своих собственных экспериментов. Архивчик .zip весит около 200Kb, что прилично для подобной библиотеки. Но пугаться не стоит &#8211; из всего архива нам потребуется только один файлик, а все остальное &#8211; это сопутствующая информация. Если распаковать архив, то увидим следующий список файлов и папок:

<pre>build\
  mixins\
  .gitignore
  .travis.yml
  bower.json
  Gruntfile.js
  LICENSE
  package.json
  README.md
  README-template.md
</pre>

Первая папка build &#8211; самая нужная, там находятся два файла lesshat.less и lesshat-prefixed.less (не успел разобраться, для чего нужен этот файл), которые являются готовыми к использованию коллекциями LESS-миксинов. Вторая папка mixins &#8211; также содержит всю коллекцию миксинов, но предназначена для разработчиков. Другими словами, если у вас есть соответствующая квалификация и желание что-то подправить в любом из миксинов, то вам сюда. Все остальные файлы можно смело пропустить, они для работы не нужны.

Теперь создаю шаблон для будущей площадки экспериментов под LESS и LESS Hat. Все как обычно &#8211; подключаю файл стилей в формате .less и файл для автоматической компиляции в CSS на лету &#8211; less-1.3.3.min.js:

<pre>...
  
  ...
</pre>

Затем вытаскиваю из папки файлик lesshat.less и кидаю его в папочку css, где также расположен файл style.less (все до кучи). Кстати, сразу оговорюсь, что все файлы и пример в целом (для этой статьи) у меня крутился под управлением локального сервера XAMPP. С ним у меня отношения сложились с первого раза, в отличие от других популярных серверов, таких как OpenServer, Endels(Denwer), WAMP.

Файл lesshat.less подключаю к style.less через директиву @import. Как говориться в оф. документации к LESS, расширение .less можно и не указывать, но оставлю &#8220;как есть&#8221;:

<pre>...
  /* Imports
  ------------------*/
  @import "lesshat.less";
  ...
</pre>

Все готово для того, чтобы опробовать библиотеку LESS Hat. Применю оттуда готовый миксин `.border-radius(10)` для создания скругленных углов у блока с помощью CSS-свойства border-radius. В документации к этому миксину говориться, что он может принимать значения без указания единиц измерения, так как допишет их сам (px по умолчанию). Также вспомним функции для работы с цветами в LESS. И воспользуемся еще двумя миксинами из LESS Hat: `.background-image()` для создания градиентов у блока и `.box-shadow()` для придания внешней тени.

Рабочий файлик style.less получиться следующим:

<pre>/* Imports
  ------------------*/
  @import "lesshat.less";

  /* Variables
  ------------------*/
  @width: 200px;
  @color: #778899;


  /* Block
  ------------------*/
  div{
    float: left;
    margin: 10px;
    text-align: center;
    width: @width;
    height: @width/2;
    .border-radius(10);
  }


  /* Colors
  ------------------*/
  .color{
    background-color: @color;
  }
  .lighten{
    background-color: lighten(@color, 20%);
  }
  .darken{
    background-color: darken(@color, 20%);
  }
  .saturate{
    background-color: saturate(@color, 20%);
  }
  .desaturate{
    background-color: desaturate(@color, 20%);
  }
  .fadein{
    background-color: fadein(@color, 20%);
  }
  .fadeout{
    background-color: fadeout(@color, 20%);
  }
  .spin-plus{
    background-color: spin(@color, 20);
  }
  .spin-minus{
    background-color: spin(@color, -20);
  }
  .gradient{
    .background-image(linear-gradient(to bottom, lighten(@color, 20%) 0%, darken(@color, 20%) 100%));
    .box-shadow(2, 2, 3, lighten(@color, 10%));
  }
</pre>

Результат работы препроцессора LESS и его библиотеки миксинов LESS Hat показан ниже. Вот это да &#8211; работает!! ))<figure id="attachment_604" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/LESSHat_border-radius-600x218.png" alt="LESS Hat - миксин .border-radius" width="600" height="218" class="size-medium wp-image-604" />][2]<figcaption class="wp-caption-text">LESS Hat &#8211; миксин .border-radius(), .background-image(), .box-shadow()</figcaption></figure> 

Список всех миксинов, доступных в этой библиотеке, представлен в начале файла `lesshat.less`, в разделе &#8220;TABLE OF MIXINS&#8221;. Количество mixin&#8217;ов немаленькое (86 штук), но мне кажется, что у Compass оно будет намного больше.

Подробное описание и примеры использования каждого из миксинов библиотеки LESS Hat доступно на GitHub в файле README.md. Добро пожаловать ознакомиться &#8211; там все хорошо описано.

В принципе &#8211; больше и сказать нечего. Подключайте и используйте LESS Hat &#8211; только так можно освоить и оценить эту библиотеку. Для себя я сделал вывод, что мне пока удобнее работать с SASS/Compass и возможностей у последнего больше, чем у LESS/LESS Hat.

Оцените статью:  
<span id="post-ratings-601" class="post-ratings" data-nonce="1b3fc7dc4b"><img id="rating_601_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(601, 1, '1 Star');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_601_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(601, 2, '2 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_601_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(601, 3, '3 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_601_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(601, 4, '4 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_601_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(601, 5, '5 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>4,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_601_text"></span></span><span id="post-ratings-601-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=131 "Compass - фреймворк под SASS (SCSS)"
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/LESSHat_border-radius.png