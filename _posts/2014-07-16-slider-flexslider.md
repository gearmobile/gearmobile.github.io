---
title: Слайдер FlexSlider
author: gearmobile
excerpt: 'Слайдер FlexSlider создан под библиотеку jQuery версии не ниже 1.4. С помощью него можно создать на странице как слайдер, так и карусель изображений. Имеет большое количество удобных настроек в самом скрипте - не нужно разбираться с DOM-деревом.'
layout: post
permalink: /slider-flexslider/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 12
ratings_score:
  - 42
ratings_average:
  - 3.5
categories:
  - 'Javascript &amp; jQuery'
tags:
  - flexslider
---
Люблю я разбирать новые слайдеры и пробовать с ними работать. На этот раз я столкнулся с неизвестным для себя плагином FlexSlider в одном из готовых HTML-макетов австралийского фрилансера [Peter Finlan][1]. Домашняя страничка слайдера FlexSlider располагается здесь &#8211; [FlexSlider 2][2]. Как сказано на официальной страничке, слайдер является адаптивным, периодически.

В арсенале у плагина заготовлена возможность автоматического генерирования перемотки изображений, пагинации страниц; показ не только изображений, но и видео. А вот **заголовок для данного слайдера не предусмотрен**, насколько я понял (*поправьте меня, если я неправ &#8211; буду только рад, ибо слайдер понравился*).

Зато у FlexSlider я впервые (*для себя*) встретил такую удобную возможность, как управление отображением стрелок перемотки или пагинацией **через опции самого слайдера**. То есть, не нужно копаться в сгенерированном коде DOM-дерева с помощью Firebug, чтобы найти там блок пагинации (*к примеру*) и отключить его через CSS-правило `display: block;`. В случае с FlexSlider все делается проще &#8211; прописал одну строчку `controlNav: false` и пагинация отключена.

### Подключение FlexSlider

Подключение плагина FlexSlider к HTML-странице производится абсолютно стандартно, как и для любого другого плагина, написанного под библиотеку jQuery (*я не забыл сказать, что FlexSlider написан под jQuery?*). В моем случае я использовал версию jQuery 1.11.1. Здесь есть небольшое ограничение &#8211; FlexSlider 2.3.0 требует для своей работы как минимум jQuery 1.4.2. Кнопка для скачивания FlexSlider находиться там же, где вся остальная информация &#8211; [FlexSlider Download][3].

Подключение FlexSlider в HTML:

<pre><!--  SCRIPTS  -->
  
  
  
  </pre>

### HTML-разметка для FlexSlider

Разметка для слайдера на странице выполняется в виде блока-обертки и маркированного списка:

<pre><!-- FLEXSLIDER -->
  

<div class="flexslider">
  <ul class="slides">
    <li>
      <img src="images/caramel.jpg"    width="800" height="504" alt="FlexSlider" title="Flexslider" />
    </li>
          
    
    <li>
      <img src="images/cheesecake.jpg" width="800" height="504" alt="FlexSlider" title="Flexslider" />
    </li>
          
    
    <li>
      <img src="images/donut.jpg"      width="800" height="504" alt="FlexSlider" title="Flexslider" />
    </li>
          
    
    <li>
      <img src="images/lemon.jpg"      width="800" height="504" alt="FlexSlider" title="Flexslider" />
    </li>
        
  </ul>
    
</div>

<!--  end flexslider  -->
  </pre>

Пример взят с официальной странички и в нем оставлены имена классов для обоих блоков, как есть. Плагин при своей инициализации генерирует два дополнительных блока:

  * ol class=&#8221;flex-control-nav&#8221; &#8211; для **пагинации** изображений
  * ul class=&#8221;flex-direction-nav&#8221; &#8211; для **стрелок перемотки** изображений

&#8230; а также создает блок-обертку `div class="flex-viewport"` для списка `ul class="slides"`. То есть, разметка получается **прозрачной и ясной**.

### Инициализация FlexSlider

Для инициализации плагина FlexSlider нужно в конфигурационном js-файле для случая **самого простого вида** написать такие строки:

<pre>$(document).ready(function(){
    $('.flexslider').flexslider({
      animation: "slide"
    });
  });
  </pre>

В принципе, уже этого достаточно для создания слайдера FlexSlider &#8211; он уже работает. Можно стилизовать его самому с помощью CSS, или же подключить уже готовые CSS-стили и отредактировать их &#8211; кому как удобно. Я попробую отредактировать внешний вид слайдера сам:

<pre>$color: #778899;

  .flexslider{
    position: relative;
    width: 800px;
    margin: 20px auto 0;
    border: 10px solid darken($color,20%);
    @include border-radius(5px);
    @include box-shadow(lighten($color,5%) 0 0 10px);

    /*  PAGINATION  */
    .flex-control-nav{
      position: relative;
      z-index: 3;
      padding: 5px 0;
      margin-top: -30px;
      @include pie-clearfix;
      @include squish-text;
      li{
        float: left;
        margin-left: 10px;
        a{
          display: block;
          width: 20px;
          height: 20px;
          background-color: lighten($color,5%);
          cursor: pointer;
          @include border-radius(50%);
          @include single-transition(background-color, .2s, ease-in-out);
          &#038;.flex-active{
            background-color: darken($color,10%);
            cursor: default;
          }
          &#038;:hover,&#038;:focus{
            background-color: darken($color,10%);
          }
        }
      }
    }

    /*  ARROWS  */
    .flex-direction-nav{
      @include squish-text;
      .flex-prev,
      .flex-next{
        position: absolute;
        top: 50%;
        margin-top: -10px;
        display: block;
        width: 20px;
        height: 20px;
        background-color: lighten($color,5%);
        border: 2px solid darken($color,10%);
        @include border-radius(50%);
        @include single-transition(background-color, .2s, ease-in-out);
        &#038;:hover,&#038;:focus{
          outline: none;
          background-color: darken($color,10%);
        }
      }
      .flex-prev{
        left: 10px;
      }
      .flex-next{
        right: 10px;
      }
    }
    /*  IMAGES  */
    .flex-viewport{
      li{
        @include box-shadow(rgba(0,0,0,.6) 0 0 8px 4px inset);
        img{
          vertical-align: top;
          position: relative;
          z-index: -2;
        }
        }
      }
    }
  </pre><figure id="attachment_1512" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/flexslider-600x403.jpg" alt="Стилизованный слайдер FlexSlider" width="600" height="403" class="size-medium wp-image-1512" />][4]<figcaption class="wp-caption-text">Стилизованный слайдер FlexSlider</figcaption></figure> 

### Опции слайдера FlexSlider

Плагин имеет большое количество настроек, которые представлены ниже. Список взят отсюда &#8211; [Flexslider &#8211; адаптивный слайдер][5].

#### Опции по умолчанию:

  * namespace: &#8220;flex-&#8220;, //{Новое} String: Префикс, прикрепляемый к классу каждого элемента сгенерированного плагином
  * selector: &#8220;.slides > li&#8221;, //{Новое} Selector: Должен соответствовать простому шаблону. &#8216;{container} > {slide}&#8217; &#8212; Игнорируйте шаблон на свой страх и риск
  * animation: &#8220;fade&#8221;, //String: Тип анимации, &#8220;fade&#8221; или &#8220;slide&#8221;
  * easing: &#8220;swing&#8221;, //{Новое} String: Определяет переход поддерживаемый плагином jQuery easing.
  * direction: &#8220;horizontal&#8221;, //String: Выбор направления смены изображений &#8220;horizontal&#8221; или &#8220;vertical&#8221;
  * reverse: false, //{NEW} Boolean: реверс направления анимации
  * animationLoop: true, //Boolean: Цикличность анимации. Если false, directionNav будет добавлять класс &#8220;disable&#8221; на обоих концах слайдера
  * smoothHeight: false, //{Новое} Boolean: Allow height of the slider to animate smoothly in horizontal mode
  * startAt: 0, //Integer: Слайд с какого должно начинаться слайдшоу. Массив (0 = первый слайд)
  * slideshow: true, //Boolean: Включение автослайдшоу
  * slideshowSpeed: 7000, //Integer: Скорость слайдшоу в мс
  * animationSpeed: 600, //Integer: Скорость анимации в мс
  * initDelay: 0, //{Новое} Integer: Задержка инициализации в мс  
    -randomize: false, //Boolean: Случайный порядок слайдов

#### Использование функций

  * pauseOnAction: true, //Boolean: Pause the slideshow when interacting with control elements, highly recommended.
  * pauseOnHover: false, //Boolean: Pause the slideshow when hovering over slider, then resume when no longer hovering
  * useCSS: true, //{Новое} Boolean: Slider will use CSS3 transitions if available
  * touch: true, //{Новое} Boolean: Allow touch swipe navigation of the slider on touch-enabled devices
  * video: false, //{Новое} Boolean: If using video in the slider, will prevent CSS3 3D Transforms to avoid graphical glitches

#### Первичное управление

  * controlNav: true, //Boolean: Создание навигации для постраничного управления каждым слайдом. Замечание: оставьте true для использования manualControls
  * directionNav: true, //Boolean: Создание навигации для кнопок назад/вперед (true/false)
  * prevText: &#8220;Previous&#8221;, //String: Тест для кнопки &#8220;previous&#8221; пункта directionNav
  * nextText: &#8220;Next&#8221;, //String: Тест для кнопки &#8220;next&#8221; пункта directionNav

#### Вторичная навигация

  * keyboard: true, //Boolean: Разрешает навигацию с помощью стрелок на клавиатуре (влево/вправо)
  * multipleKeyboard: false, //{Новое} Boolean: Разрешает управление с помощью клавиатуры по несколькими слайдерами. Поведение по умолчанию вырезает возможность управления клавиатурой при использовании более одного слайдера
  * mousewheel: false, //{Обновление} Boolean: Требуется плагин jquery.mousewheel.js (https://github.com/brandonaaron/jquery-mousewheel) &#8211; Управление навигацией по слайдам с помощью колесика мыши
  * pausePlay: false, //Boolean: Создание динамического pause/play элемента
  * pauseText: &#8220;Pause&#8221;, //String: Текста для кнопки &#8220;pause&#8221; элемента pausePlay
  * playText: &#8220;Play&#8221;, //String: Текст для кнопки &#8220;play&#8221; элемента pausePlay

#### Специальные свойства

  * controlsContainer: &#8220;&#8221;, //{Обновление} jQuery Object/Selector: Объявление какой контейнер элементов навигации будет применен. По умолчанию это FlexSlider. Например, можно использовать так $(&#8220;.flexslider-container&#8221;). Свойство игнорируется если элемент не найден.
  * manualControls: &#8220;&#8221;, //{Обновление} jQuery Object/Selector: Объявление пользовательской панели управления навигацией. Примером может быть $(&#8220;.flex-control-nav li&#8221;) или &#8220;#tabs-nav li img&#8221;, и т.п.. Количество элементов в вашей controlNav должно совпадать с количеством слайдов/табов.
  * sync: &#8220;&#8221;, //{Новое} Selector: Зеркало действий выполняемых над этим слайдером с помощью другого слайдера. Используйте с осторожностью.
  * asNavFor: &#8220;&#8221;, //{Новое} Selector: Внутренние свойства направленные на превращение слайдера в миниатюры с возможностью навигации для другого слайдера

#### Опции карусели

  * itemWidth: 0, //{Новое} Integer: Ширина Box-model отдельных элементов карусели, включая горизонтальные границы и отступы (padding)
  * itemMargin: 0, //{Новое} Integer: Отступ между элементами карусели
  * minItems: 0, //{Новое} Integer: Минимальное количество элементов карусели, которые будут видимы. Элементы будут плавно изменять размер при значении ниже заданного
  * maxItems: 0, //{Новое} Integer: Максимальное количество элментов карусели, которые будут видимы. Элементы будут плавно изменять размер при превышении этого лимита.
  * move: 0, //{Новое} Integer: Количество элментов в карусели, которые должны двигаться по анимации. Если 0, то слайдер будет двигать все видимые элементы

#### Callback API

  * start: function(){}, //Callback: function(slider) &#8211; Срабатывает, когда слайдер загружает первый слайд
  * before: function(){}, //Callback: function(slider) &#8211; Срабатывает асинхронно с каждой анимацией слайдера
  * after: function(){}, //Callback: function(slider) &#8211; Срабатывает после каждой завершенной анимацией слайдера
  * end: function(){}, //Callback: function(slider) &#8211; Срабатывает, когда слайдер доходит до последнего элемента (асинхронный)
  * added: function(){}, //{Новое} Callback: function(slider) &#8211; Срабатывает после того, как слайд добавлен
  * removed: function(){} //{Новое} Callback: function(slider) &#8211; Срабатывает после того, когда слайд удален

### Варианты слайдера FlexSlider

На официальной страничке плагина в прекрасно оформленном виде представлены [различные варианты][6] создания слайдера. Все они реализуются с помощью опций этого плагина и дополнительной HTML-разметки.

Например, чтобы создать слайдер с thumbnail-пагинацией, нужно прописать в js-файле настроек:

<pre>$('.flexslider').flexslider({
    animation: "slide",
    controlNav: "thumbnails"
  });
  </pre>

&#8230; а HTML-разметку изменить таким образом:

<pre><!-- Place somewhere in the <body> of your page -->
  

<div class="flexslider">
  <ul class="slides">
    <li data-thumb="slide1-thumb.jpg">
      <img src="slide1.jpg" />
            
    </li>
          
    
    <li data-thumb="slide2-thumb.jpg">
      <img src="slide2.jpg" />
            
    </li>
          
    
    <li data-thumb="slide3-thumb.jpg">
      <img src="slide3.jpg" />
            
    </li>
          
    
    <li data-thumb="slide4-thumb.jpg">
      <img src="slide4.jpg" />
            
    </li>
        
  </ul>
    
</div>
  </pre>

Но, в принципе, в этом случае рассказывать о возможных вариантах слайдера достаточно глупо &#8211; можно и нужно посетить официальную страничку и там смотреть примеры создания.

На этом все.

Оцените статью:  
<span id="post-ratings-1510" class="post-ratings" data-nonce="85616329ea"><img id="rating_1510_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1510, 1, '1 Star');" onmouseout="ratings_off(3.5, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1510_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1510, 2, '2 Stars');" onmouseout="ratings_off(3.5, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1510_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1510, 3, '3 Stars');" onmouseout="ratings_off(3.5, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1510_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1510, 4, '4 Stars');" onmouseout="ratings_off(3.5, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1510_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1510, 5, '5 Stars');" onmouseout="ratings_off(3.5, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>12</strong> votes, average: <strong>3,50</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1510_text"></span></span><span id="post-ratings-1510-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://peterfinlan.com/ "Peter Finlan"
 [2]: http://flexslider.woothemes.com/index.html "FlexSlider 2"
 [3]: http://flexslider.woothemes.com/index.html "FlexSlider Download"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/07/flexslider.jpg
 [5]: http://pcvector.net/scripts/slideshow_and_scroller/386-flexslider-adaptivnyy-slayder.html "Flexslider - адаптивный слайдер"
 [6]: http://flexslider.woothemes.com/index.html ""