---
title: Слайдер jqFancyTransitions
author: gearmobile
excerpt: 'Данная статья посвящена обзору слайдера jqFancyTransitions - его установке, настройке и стилизации. Слайдер jqFancyTransitions основан на библиотеке jQuery (впрочем, как и подавляющее большинство слайдеров подобного типа). Слайдер jqFancyTransitions предоставляет стандартный набор органов управления слайдшоу - кнопки перемотки взад-вперед, пагинация и показ заголовка картинки. Помимо этого имеется возможность сделать изображения в слайдере ссылками.'
layout: post
permalink: /%d1%81%d0%bb%d0%b0%d0%b9%d0%b4%d0%b5%d1%80-jqfancytransitions/
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
  - слайдер jqFancyTransitions
---
Данная статья посвящена обзору слайдера jqFancyTransitions &#8211; его установке, настройке и стилизации. Слайдер jqFancyTransitions основан на библиотеке jQuery (впрочем, как и подавляющее большинство слайдеров подобного типа). Эффекты, применимые к данному слайдеру, можно посмотреть на домашней странице проекта &#8211; [jqFancyTransitions][1]. Их достаточное количество &#8211; wave, zipper, curtain, curtain alternate, fountain top, random top, left top, right bottom. Слайдер jqFancyTransitions предоставляет стандартный набор органов управления слайдшоу &#8211; кнопки перемотки взад-вперед, пагинация и показ заголовка картинки. Помимо этого имеется возможность сделать изображения в слайдере ссылками.

### Установка слайдера jqFancyTransitions

Для подключения слайдера jqFancyTransitions в рабочий проект необходимо выполнить стандартные операции:

  * подключить библиотеку jQuery
  * подключить плагин jqFancyTransitions

<pre></pre>

В данной статье проверялась совместная работа плагина jqFancyTransitions с библиотекой jQuery версии 1.10.1. Другие версии jQuery не &#8220;испытывались&#8221;, поэтому о их работоспособности с этим плагином ничего сказать не могу. Естественно, подключать jQuery можно разными путями &#8211; локально или через разнообразные CDN, это уж кому как нравиться.

Затем создаем разметку для слайдера jqFancyTransitions в HTML-документе:

<pre><div id="slider">
  <img src="http://placehold.it/400x300/c8c8c8/fff" alt="Mascot 1" />
      <img src="http://placehold.it/400x300/b8b8b8/fff" alt="Mascot 2" />
      <img src="http://placehold.it/400x300/a8a8a8/fff" alt="Mascot 3" />
      <img src="http://placehold.it/400x300/989898/fff" alt="Mascot 4" />
      <img src="http://placehold.it/400x300/888888/fff" alt="Mascot 5" />
      <img src="http://placehold.it/400x300/787878/fff" alt="Mascot 6" />
    
</div>
  </pre>

Как видим, разметка чрезвычайно минималистична &#8211; блок-обертка с обязательным идентификатором id (если использовать класс вместо идентификатора, плагин jqFancyTransitions работать не будет) и набор изображений img. В данном примере я воспользовался сервисом [Placehold.it][2] для быстрого и удобного способа эмуляции картинок в проекте.

Минималистичность HTML-разметки для работы плагина jqFancyTransitions &#8211; с точки зрения HTML-семантики просто прекрасно; а вот с точки зрения web-разработчика &#8211; не очень, так как придется в дальнейшем воспользоваться плагином [Firebug][3] под Mozilla Firefox, чтобы решить проблему стилизации слайдера jqFancyTransitions.

### Настройка слайдера jqFancyTransitions

Как любой слайдер подобного рода, jqFancyTransitions имеет набор опций для настройки своей работы. Можно управлять скоростью показа картинок, выбрать нужный эффект перехода, отобразить или скрыть элементы управления slideshow. Полный список настроек представлен ниже:

<pre>effect: '', // wave, zipper, curtain ( волны, застежка, занавес)
  width: 500, // ширина панели
  height: 332, // высота панели
  strips: 20, // количество полос
  delay: 5000, // задержка между сменой изображений в ms
  stripDelay: 50, // задежка между эффектами в ms
  titleOpacity: 0.7, // прозрачность подписи (title)
  titleSpeed: 1000, // время показа подписи в ms
  position: 'alternate', // top, bottom, alternate, curtain
  direction: 'fountainAlternate', // left, right, alternate, random, fountain, fountainAlternate
  navigation: false, // кнопки навигации prev и next
  links: false // показ картинок как ссылок
  </pre>

Настройка плагина jqFancyTransitions производится в отдельном js-файле с произвольным именем, который также подключается в проект **после** библиотеки jQuery и плагина jqFancyTransitions. В моем случае я создал js-файл с именем script:

<pre></pre>

&#8230; и наполнил его первоначальным содержимым:

<pre>$(document).ready(function(){
      $('#slider').jqFancyTransitions({
        width: 400,
        height: 300,
        navigation: true
      });
  });
  </pre>

То есть, я задал для обертки с идентификатором `#slider` высоту и ширину через параметры `height: 300`, `width: 400`; также задал, что данный слайдер должен иметь органы управления &#8211; пагинацию и кнопки перемотки слайдшоу &#8211; `navigation: true`.

Отлично! Уже сейчас наш плагин должен работать:<figure id="attachment_1357" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/jqFancyTransitions_first-view-600x374.jpg" alt="Слайдер jqFancyTransitions - первый запуск" width="600" height="374" class="size-medium wp-image-1357" />][4]<figcaption class="wp-caption-text">Слайдер jqFancyTransitions &#8211; первый запуск</figcaption></figure> 

Видим, что плагин jqFancyTransitions создал слайдшоу из шести картинок размером 400x300px, как я и прописывал в HTML-разметке. Помимо этого, плагином были сгенерированы кнопки перемотки взад-вперед (`prev` и `next`), пагинация (номера 1,2,3,4,5,6 внизу слайдера) и заголовок изображения (`title`).

Теперь осталось привести наш слайдер к тому виду, который необходим. В данном конкретном случае мне необходимо убрать кнопки перемотки, заголовок изображений; кнопки пагинации стилизовать и переместить вовнутрь слайдера. Этим я и займусь в следующей части данного обзора.

### Стилизация слайдера jqFancyTransitions

Для придания слайдеру jqFancyTransitions необходимого внешнего вида я воспользуюсь своим любимым Sass/Compass. Также для задачи стилизации слайдера потребуется плагин Firebug &#8211; незаменимая штука для web-разработчика. В моем случае этот плагин понадобиться для определения имен идентификаторов и классов HTML-элементов, которые генерирует плагин jqFancyTransitions.

Чтобы было понятно, о чем идет речь, давайте взглянем на снимок окна браузера с запущенным плагином Firebug, который я сделал для данного примера. Посмотрим на вкладку HTML &#8211; там есть элементы, которые первоначально не присутствуют в нашей HTML-разметке:<figure id="attachment_1358" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/jqFancyTransitions_Firebug-600x485.jpg" alt="Слайдер jqFancyTransitions под прицелом Firebug" width="600" height="485" class="size-medium wp-image-1358" />][5]<figcaption class="wp-caption-text">Слайдер jqFancyTransitions под прицелом Firebug</figcaption></figure> 

Убираю кнопки перемотки и заголовок изображения. Для этого с помощью Firebug нахожу имена идентификаторов этих элементов и прописываю для них правила:

<pre>#ft-prev-slider,#ft-next-slider,#ft-title-slider{
    display: none;
  }
  </pre>

Пагинацию изображений `#ft-buttons-slider` перемещаю вверх и влево:

<pre>#ft-buttons-slider{
    position: relative;
    top: -40px;
    right: 5px;
    padding-top: 0 !important;
    ...
  </pre>

Здесь стоит обратить внимание на последнее правило обнуления верхнего `padding` &#8211; для него потребовалось суровая мера в виде `!important`, чтобы переопределить внутренние стили, задаваемые самим плагином jqFancyTransitions для данного HTML-элемента.

Для кнопок пагинации `.ft-button-slider` задаю размер, фоновую заливку и расстояние между ними:

<pre>.ft-button-slider{
    text-decoration: none;
    font-size: 12px;
    color: darken(#fff,10%);
    background-color: $color;
    margin-left: 10px;
    @include text-shadow(rgba(0,0,0,.5) 1px 1px 0);
  </pre>

Чтобы выделить активную кнопку в пагинации, создаю для генерируемого плагином jqFancyTransitions класса `.ft-button-slider-active` правила:

<pre>.ft-button-slider-active{
    background-color: darken($color,10%);
    color: #fff;
  }
  </pre>

Начиная с версии 1.7 плагин jqFancyTransitions позволяет создавать из изображений слайдера ссылки. То есть, картинки, мелькающие в виде slideshow, одновременно являются ссылками. Чтобы сделать так, достаточно в HTML-разметке дописать теги ссылок:

<pre><div id="slider">
  <img src="http://placehold.it/400x300/c8c8c8/fff" alt="Mascot 1" /><a href="http://localhost:7788/third/"></a>
      <img src="http://placehold.it/400x300/b8b8b8/fff" alt="Mascot 2" /><a href="http://localhost:7788/third/"></a>
      <img src="http://placehold.it/400x300/a8a8a8/fff" alt="Mascot 3" /><a href="http://localhost:7788/third/"></a>
      <img src="http://placehold.it/400x300/989898/fff" alt="Mascot 4" /><a href="http://localhost:7788/third/"></a>
      <img src="http://placehold.it/400x300/888888/fff" alt="Mascot 5" /><a href="http://localhost:7788/third/"></a>
      <img src="http://placehold.it/400x300/787878/fff" alt="Mascot 6" /><a href="http://localhost:7788/third/"></a>
    
</div>
  </pre>

&#8230; а в файле настроек `script.js` плагина jqFancyTransitions добавить строку `links: true`:

<pre>$(document).ready(function(){
    $('#slider').jqFancyTransitions({
      width: 400,
      height: 300,
      navigation: true,
      links: true
    });
  });
  </pre>

Можно немного приукрасить слайдер, изменив эффект смены изображений с `zipper` на `curtain` &#8211; `effect: 'curtain'` и уменьшив задержку по времени при смене изображений `delay: 2000`:

<pre>$(document).ready(function(){
    $('#slider').jqFancyTransitions({
      width: 400,
      height: 300,
      navigation: true,
      effect: 'curtain',
      delay: 2000,
      links: true
    });
  });
  </pre>

Дополнительные CSS3-украшательства можно добавить по вкусу, желанию и необходимости.

### Готовый слайдер jqFancyTransitions

Примерный результат создания слайдера jqFancyTransitions может выглядеть таким образом:<figure id="attachment_1359" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/ready_jqFancyTransitions-600x394.jpg" alt="Готовый слайдер jqFancyTransitions" width="600" height="394" class="size-medium wp-image-1359" />][6]<figcaption class="wp-caption-text">Готовый слайдер jqFancyTransitions</figcaption></figure> 

Ниже показан готовый код, с помощью которого создавался подобный слайдер.

HTML-код:

<pre>
  

<div class="wrapper">
  <div id="slider">
    <img src="http://placehold.it/400x300/c8c8c8/fff" alt="Mascot 1" /><a href="http://localhost:7788/third/"></a>
          <img src="http://placehold.it/400x300/b8b8b8/fff" alt="Mascot 2" /><a href="http://localhost:7788/third/"></a>
          <img src="http://placehold.it/400x300/a8a8a8/fff" alt="Mascot 3" /><a href="http://localhost:7788/third/"></a>
          <img src="http://placehold.it/400x300/989898/fff" alt="Mascot 4" /><a href="http://localhost:7788/third/"></a>
          <img src="http://placehold.it/400x300/888888/fff" alt="Mascot 5" /><a href="http://localhost:7788/third/"></a>
          <img src="http://placehold.it/400x300/787878/fff" alt="Mascot 6" /><a href="http://localhost:7788/third/"></a>
        
  </div>
    
</div>

<!-- end wrapper -->
  
  </pre>

SCSS-код:

<pre>@import "compass/reset";
  @import "compass/css3/text-shadow";
  @import "compass/css3/box-shadow";

  $color: #778899;

  .wrapper{
    margin: 50px auto;
    width: 420px;
    #slider{
      border: 10px solid rgba(0,0,0,.5);
      @include box-shadow(rgba(0,0,0,.8) 2px 2px 10px);
      #ft-prev-slider,#ft-next-slider,#ft-title-slider{
        display: none;
      }
    }
    #ft-buttons-slider{
      position: relative;
      top: -40px;
      right: 5px;
      padding-top: 0 !important;
      .ft-button-slider{
        text-decoration: none;
        font-size: 12px;
        color: darken(#fff,10%);
        background-color: $color;
        margin-left: 10px;
        @include text-shadow(rgba(0,0,0,.5) 1px 1px 0);
        &#038;:first-child{
          margin-left: 0;
        }
        &#038;:focus,&#038;:active{
          outline: none;
        }
        &#038;:hover{
          color: lighten($color,40%);
          background-color: lighten($color,10%);
        }
      }
      .ft-button-slider-active{
        background-color: darken($color,10%);
        color: #fff;
      }
    }
  }
  </pre>

JavaScript-код:

<pre>$(document).ready(function(){
      $('#slider').jqFancyTransitions({
        width: 400,
        height: 300,
        navigation: true,
        effect: 'curtain',
        delay: 2000,
        links: true
      });
  });
  </pre>

На этом все &#8211; удачного кодинга!

Оцените статью:  
<span id="post-ratings-1354" class="post-ratings" data-nonce="0496fe807b"><img id="rating_1354_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1354, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1354_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1354, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1354_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1354, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1354_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1354, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1354_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1354, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_1354_text"></span></span><span id="post-ratings-1354-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://workshop.rs/projects/jqfancytransitions/ "jqFancyTransitions"
 [2]: http://placehold.it/ "Placehold.it"
 [3]: https://addons.mozilla.org/ru/firefox/addon/firebug/ "Firebug"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/06/jqFancyTransitions_first-view.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2014/06/jqFancyTransitions_Firebug.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/06/ready_jqFancyTransitions.jpg