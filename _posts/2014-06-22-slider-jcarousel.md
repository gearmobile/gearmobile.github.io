---
title: Слайдер jCarousel
author: gearmobile
excerpt: 'Плагин jCarousel по популярности в списке плагинов типа carousel занимает второе место после скрипта slick.  Плагин jCarousel основан на библиотеке jQuery и предоставляет стандартные возможности управления показом картинок - кнопки перемотки взад-вперед и пагинация картинок. Показ заголовка картинки не предусмотрен, но имеется возможность автопрокрутки изображений.'
layout: post
permalink: /slider-jcarousel/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 8
ratings_score:
  - 36
ratings_average:
  - 4.5
categories:
  - 'Javascript &amp; jQuery'
tags:
  - jCarousel
---
Данная статья посвящена обзору еще одного js-плагина для создания slideshow из картинок &#8211; jCarousel. Автором данного скрипта является [Jan Sorgalla][1]. Хотя мне эти имя и фамилия ни о чем не говорит, но они запоминающиеся. Название данного плагина я запомнил по имени его автора раньше, чем по имени самого скрипта. Это было типа шутки, конечно&#8230; )))

Скрипт jCarousel по популярности в списке плагинов типа carousel занимает второе место после скрипта slick &#8211; [jQuery Plugins][2]. Кто вдруг не знает, термин carousel (карусель) является общим описанием плагинов и скриптов подобного типа. Плагин jCarousel основан на библиотеке jQuery и предоставляет стандартные возможности управления показом картинок &#8211; кнопки перемотки взад-вперед и пагинация картинок. Показ заголовка картинки не предусмотрен, но имеется возможность автоскроллинга изображений.

### Особенности плагина jCarousel

Первая особенность плагина заключается в том, что здесь почти ничего не генерируется автоматически, самим скриптом jCarousel. Только пагинация создается с помощью js-кода, все остальное нужно прописывать вручную в HTML-коде. Для меня это было весьма огорчительно, так как такой подход занимает много времени и сил.

Вторая особенность плагина &#8211; он имеет модульную структуру. То есть, имеется основная составляющая скрипта jCarousel &#8211; `jquery.jcarousel-core.min.js`, которая на то и является основной, что предоставляет базовые возможности для создания слайдшоу. Если необходимо к слайдшоу добавить возможность прокрутки, то нужно скачать и подключить модуль `jquery.jcarousel-control.min.js`. Для включения возможности пагинации необходим еще один модуль &#8211; `jquery.jcarousel-pagination.min.js`. Для автоскролинга потребуется модуль `jquery.jcarousel-autoscroll.min.js`.

В проекте перечисленные выше модули подключаются последовательно, в таком порядке (первые два пункта строго обязательны, остальные могут добавляться, убираться и перемещаться между собой произвольно):

  * библиотека jQuery &#8211; jquery-1.11.1.min.js
  * основной модуль jCarousel Core &#8211; jquery.jcarousel-core.min.js
  * модуль прокрутки &#8211; jquery.jcarousel-control.min.js
  * модуль пагинации &#8211; jquery.jcarousel-pagination.min.js
  * модуль автоскроллинга &#8211; jquery.jcarousel-autoscroll.min.js

Справедливости стоит сказать, что можно не заморачиваться с отдельными модулями и подключить все одним файлом, по типу &#8220;все включено&#8221; &#8211; `jquery.jcarousel.min.js`:

  * библиотека jQuery &#8211; jquery-1.11.1.min.js
  * плагин jCarousel со всеми его возможностями &#8211; jquery.jcarousel.min.js

Страница для скачивания плагина jCarousel одним файлом (Full Download) или отдельными его модулями (Separate Downloads) расположена здесь &#8211; [jCarousel Dist][3]. Можно получить как Production Version (compressed), так и Development Version (uncompressed). В данной статье будут использоваться сжатые версии скрипта, так как в исходном коде плагина копаться не будем.

Плагин требует для своей работы библиотеку jQuery **версии не ниже 1.7** &#8211; это также стоит учесть.

### Подключение плагина jCarousel

Создаем набросок HTML-страницы и производим подключение плагина jCarousel. Для чистоты и наглядности буду применять подход модульности плагина. Как и любой другой плагин подобного рода, его управление производится через отдельный js-файл произвольного имени, в котором прописываются параметры скрипта. Я создал для этой цели js-файл `simple.js` и выполнил подключение таким образом:

<pre></pre>

Шкурка `style.css` служит для стилизации слайдера jCarousel на HTML-странице, то есть в этом файле будут писаться CSS-стили для всех элементов слайдера jCarousel.

### Базовая разметка слайдера jCarousel

Плагин для своей работы требует некоторую **обязательную базовую HTML-разметку** и **CSS-стили к ней**. HTML-разметка может быть не обязательно именно такой, как представлена ниже, но основная ее структура должна сохраняться:

<pre><div class="jcarousel">
  <ul>
    <li>
      <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 1" alt="" />
    </li>
          
    
    <li>
      <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 2" alt="" />
    </li>
          
    
    <li>
      <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 3" alt="" />
    </li>
          
    
    <li>
      <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 4" alt="" />
    </li>
          
    
    <li>
      <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 5" alt="" />
    </li>
          
    
    <li>
      <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 6" alt="" />
    </li>
        
  </ul>
    
</div>

<!--  end jcarousel  -->
  </pre>

То есть, должен присутствовать блок-обертка с классом `class="jcarousel"` (имя класса может быть произвольным), внутри которого должен находиться еще один блок-обертка. И затем только идут элементы с картинками. HTML-структура, надо сказать, несколько громоздкая по стандартам сегодняшнего времени.

К обязательной базовой HTML-разметке &#8220;прилагаются&#8221; не менее обязательные CSS-стили (*меня эти обязательства уже начинают удручать*):

<pre>.jcarousel {
    position: relative;
    overflow: hidden;
    ul{
      width: 20000em;
      position: relative;
      li{
        float: left;
      }
    }
  }
  </pre>

Код выше &#8211; это конечно не совсем CSS-код. Это SCSS, но наглядность (как мне кажется) от этого только выигрывает из-за ярко выраженного nesting, присущего Sass. По крайней мере, ничего не стоит за 5-10 секунд вручную перевести этот SCSS в обычный CSS, если кого вдруг это не устраивает.

В данном примере я воспользовался сервисом [Placehold.it][4] для быстрой и удобной генерации картинок в создаваемом слайдшоу.

Для активации слайдера в файле настроек `simple.js` скрипта jCarousel нужно прописать его инициализацию:

<pre>$(function() {

    // Инициализация слайдера
    $('.jcarousel').jcarousel({
        // Базовые настройки скрипта пишутся здесь
    });

  });
  </pre>

Слайдер уже готов! Правда, увидеть его работу не получиться, так как не заданы настройки скрипта, не созданы элементы для его управления. Приступим к созданию элементов управления слайдера jCarousel.

### Создание кнопок прокрутки в jCarousel

Как я уже упоминал ранее, при создании слайдера придется все создавать вручную, прописывая нужные HTML-элементы внутри HTML-документа.

Какой уважающий себя слайдер картинок может существовать без кнопок перемотки изображений взад-вперед? Конечно &#8211; никакой! Поэтому потребуется их создать.

Для этого ниже блока со слайдером дописываю две ссылки с классами `class="jcarousel-prev"` и `class="jcarousel-prev"`:

<pre><div class="wrap_jcarousel">
  <div class="jcarousel">
    <ul>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 1" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 2" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 3" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 4" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 5" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 6" alt="" />
      </li>
            
    </ul>
        
  </div>
  
  <!--  end jcarousel  -->
  
      
  
  <!--  CONTROLS  -->
      
  
  <a class="jcarousel-prev" href="#">Prev</a>
      <a class="jcarousel-next" href="#">Next</a>
  
    
</div>

<!--  end wrap_jcarousel  -->
  </pre>

Блок слайдера, элементы прокрутки (и другие будущие элементы управления слайдером) я поместил внутрь одного общего блока-обертки `class="wrap_jcarousel"`, которому придал несложные CSS-стили:

<pre>.wrap_jcarousel{
    width: 600px;
    margin: 10px auto;
    position: relative;
  </pre>

Кнопки перемотки внутри HTML-разметки созданы, однако необходимо прикрутить к ним действия с помощью js-скрипта. Для этого сначала подключаю модуль прокрутки `jquery.jcarousel-control.min.js` в HTML-документе:

<pre></pre>

&#8230; а затем в файле настроек `simple.js` активирую возможность прокрутки слайдера, добавив базовые js-строки:

<pre>$(function() {
    $('.jcarousel').jcarousel({
        // Базовые настройки скрипта пишутся здесь
    });

    // Инициализация прокрутки слайдера
    $('.jcarousel-prev').jcarouselControl({
        target: '-=1'
    });

    $('.jcarousel-next').jcarouselControl({
        target: '+=1'
    });
  });
  </pre>

После стилизации элементов управления и блока-обертки `class="wrap_jcarousel"` слайдер jCarousel может принять следующий вид:<figure id="attachment_1369" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/jCarousel_prev-next-600x394.jpg" alt="Слайдер jCarousel с кнопками прокрутки" width="600" height="394" class="size-medium wp-image-1369" />][5]<figcaption class="wp-caption-text">Слайдер jCarousel с кнопками прокрутки</figcaption></figure> 

Попробуем прокрутить картинки взад и вперед с помощью кнопок &#8211; все работает!

### Добавление пагинации в слайдере jCarousel

Для добавления пагинации в слайдере нужно создать в HTML-разметке дополнительный блок с классом `class="jcarousel-pagination"`:

<pre><div class="wrap_jcarousel">
  <div class="jcarousel">
    <ul>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 1" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 2" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 3" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 4" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 5" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 6" alt="" />
      </li>
            
    </ul>
        
  </div>
  
  <!--  end jcarousel  -->
  
      
  
  <!--  CONTROLS  -->
      
  
  <a class="jcarousel-prev" href="#">Prev</a>
      <a class="jcarousel-next" href="#">Next</a>
  
      <!--  PAGINATION  -->
      
  
  <p class="jcarousel-pagination">
    
  </p>
  
    
</div>

<!--  end wrap_jcarousel  -->
  </pre>

Больше ничего в него добавлять не нужно &#8211; плагин сам сгенерирует (*наконец-то сам что создаст!*) его содержимое. Нам только необходимо подключить соответствующий модуль `jquery.jcarousel-pagination.min.js` для пагинации в слайдере:

<pre></pre>

&#8230; а затем активировать его в файле настроек `simple.js`:

<pre>$(function() {

    // Инициализация слайдера
    $('.jcarousel').jcarousel({
        // Базовые настройки скрипта пишутся здесь
    });

    // Инициализация прокрутки слайдера
    $('.jcarousel-prev').jcarouselControl({
        target: '-=1'
    });

    $('.jcarousel-next').jcarouselControl({
        target: '+=1'
    });

    // Инициализация пагинации слайдера
    $('.jcarousel-pagination').jcarouselPagination({
        item: function(page) {
            return '<a href="#' + page + '">' + page + '</a>';
        }
    });

  });
  </pre>

Для стилизации пагинации с данном случае потребуется плагин Firebug под Mozilla Firefox для инспекции генерируемых скриптом jCarousel элементов. Примерный вид слайдера после применения некоторых CSS-стилей может быть таким:<figure id="attachment_1368" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/jCarousel_pagination-600x394.jpg" alt="Слайдер jCarousel с пагинацией" width="600" height="394" class="size-medium wp-image-1368" />][6]<figcaption class="wp-caption-text">Слайдер jCarousel с пагинацией</figcaption></figure> 

Проверим работу пагинации и &#8220;пощелкаем&#8221; на кнопках с циферками &#8211; все работает!

### Добавление автопрокрутки в jCarousel

Для автоматической прокрутки изображений в слайдере достаточно выполнить два несложных действия, которые выполнялись и ранее.

Первое &#8211; подключить модуль автопрокрутки `jquery.jcarousel-autoscroll.min.js`:

<pre></pre>

Второе &#8211; активировать автопрокрутку в файле настроек `simple.js`:

<pre>$(function() {

    // Инициализация слайдера
    $('.jcarousel').jcarousel({
        // Базовые настройки скрипта пишутся здесь
    });

    // Инициализация прокрутки слайдера
    $('.jcarousel-prev').jcarouselControl({
        target: '-=1'
    });

    $('.jcarousel-next').jcarouselControl({
        target: '+=1'
    });

    // Инициализация пагинации слайдера
    $('.jcarousel-pagination').jcarouselPagination({
        item: function(page) {
            return '<a href="#' + page + '">' + page + '</a>';
        }
    });

    // Автопрокрутка слайдера
    $('.jcarousel').jcarouselAutoscroll({
        interval: 3000,
        target: '+=1',
        autostart: true
    });

  });
  </pre>

Перезапускаю браузер, в котором открыт создаваемый мною слайдер и любуюсь результатом.

### Дополнительные украшательства для jCarousel

Что еще можно сделать для созданного слайдера jCarousel? Можно добавить стили для неактивной кнопки прокрутки изображений и для активной кнопки пагинации. Активность и неактивность этих кнопок можно отслеживать в помощью js-строк и &#8220;вешать&#8221; на нужные состояния кнопок соответствующие CSS-классы.

Для этого файл `simple.js` преобразую таким образом:

<pre>$(function() {

    // Инициализация слайдера
    $('.jcarousel').jcarousel({
        // Базовые настройки скрипта пишутся здесь
    });

    // Прокрутка слайдера

    // Кнопка PREV
    $('.jcarousel-prev')
    // Триггер класса inactive
    .on('jcarouselcontrol:active', function() {
        $(this).removeClass('inactive');
    })
    .on('jcarouselcontrol:inactive', function() {
        $(this).addClass('inactive');
    })
    // Инициализация кнопки PREV
    .jcarouselControl({
        target: '-=1'
    });

    // Кнопка NEXT
    $('.jcarousel-next')
    // Триггер класса inactive
    .on('jcarouselcontrol:active', function() {
        $(this).removeClass('inactive');
    })
    .on('jcarouselcontrol:inactive', function() {
        $(this).addClass('inactive');
    })
    // Инициализация кнопки NEXT
    .jcarouselControl({
        target: '+=1'
    });

    // Пагинация слайдера
    $('.jcarousel-pagination')
    // Триггер класса active
    .on('jcarouselpagination:active', 'a', function() {
        $(this).addClass('active');
    })
    .on('jcarouselpagination:inactive', 'a', function() {
        $(this).removeClass('active');
    })
    // Инициализация пагинации
    .jcarouselPagination({
        item: function(page) {
            return '<a href="#' + page + '">' + page + '</a>';
        }
    });

    // Автопрокрутка слайдера
    $('.jcarousel').jcarouselAutoscroll({
        interval: 3000,
        target: '+=1',
        autostart: true
    });

  });
  </pre>

&#8230; а в `style.scss` добавлю строки:

<pre>/*  PREV NEXT BUTTONS  */
  .jcarousel-prev,
  .jcarousel-next{
    position: absolute;
    top: 200px;
    ...
    &#038;.inactive{
      cursor: default;
    }
  }
  ...
  /*  PAGINATION  */
  .jcarousel-pagination{
    background-color: transparent;
    position: absolute;
    ...
      &#038;.active{
        opacity: .7;
      }
    }
  </pre>

Теперь при автоматической прокрутке изображений активная кнопка пагинации будет выделяться цветом. А при достижении конца прокрутки кнопка прокрутки становится неактивной, что визуально отмечается изменением вида курсора мыши при его наведении на кнопку.

### Заключение jCarousel

В заключение можно сказать, что на странице примеров [Examples][7] есть богатый материал для дополнительных экспериментов. В частности, интерес представляет адаптивная Responsive Carousel, которая изменяет количество картинок внутри блока в зависимости от ширины окна браузера.

Полный код рассмотренного в данной статье примера создания слайдера приведен ниже.

HTML-код:

<pre>

  

<div class="wrap_jcarousel">
  <div class="jcarousel">
    <ul>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 1" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 2" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 3" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 4" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 5" alt="" />
      </li>
              
      
      <li>
        <img src="http://placehold.it/600x400/778899/fff&#038;text=Slide 6" alt="" />
      </li>
            
    </ul>
        
  </div>
  
  <!--  end jcarousel  -->
  
      
  
  <!--  CONTROLS  -->
      
  
  <a class="jcarousel-prev" href="#">Prev</a>
      <a class="jcarousel-next" href="#">Next</a>
  
      <!--  PAGINATION  -->
      
  
  <p class="jcarousel-pagination">
    
  </p>
  
    
</div>

<!--  end wrap_jcarousel  -->
  </pre>


<p>
  SCSS-код:
</p>


<pre>
  @import "compass/reset";
  @import "compass/css3/border-radius";
  @import "compass/css3/box-shadow";
  @import "compass/typography/links/hover-link";
  @import "compass/typography/text/replacement";

  $nav_width: 30px;
  $nav_height: $nav_width;

  .wrap_jcarousel{
    width: 600px;
    margin: 10px auto;
    position: relative;
    border: 10px solid rgba(0,0,0,.5);
    @include border-radius(10px);
    @include box-shadow(rgba(0,0,0,.3) 2px 2px 10px);
    .jcarousel {
      position: relative;
      overflow: hidden;
      width: 600px;
      height: 400px;
      ul{
        width: 20000em;
        position: relative;
        li{
          float: left;
          img{
            vertical-align: top;
          }
        }
      }
    }

    /*  PREV NEXT BUTTONS  */
    .jcarousel-prev,
    .jcarousel-next{
      position: absolute;
      top: 200px;
      display: block;
      width: $nav_width;
      height: $nav_height;
      background-color: #778899;
      @include border-radius(50%);
      @include squish-text;
      @include box-shadow(rgba(0,0,0,.8) 0 0 4px inset);
      &#038;:hover{
        background-color: darken(#778899,10%);
      }
      &#038;.inactive{
        cursor: default;
      }
    }
    .jcarousel-prev{
      left: -50px;
    }
    .jcarousel-next{
      right: -50px;
    }

    /*  PAGINATION  */
    .jcarousel-pagination{
      background-color: transparent;
      position: absolute;
      bottom: 10px;
      left: 10px;
      a{
        text-decoration: none;
        text-align: center;
        line-height: 20px;
        color: #fff;
        display: inline-block;
        width: 20px;
        height: 20px;
        background-color: rgba(0,0,0,.8);
        @include border-radius(50%);
        margin-left: 5px;
        &#038;:first-child{
          margin-left: 0;
        }
        &#038;:hover{
          background-color: rgba(0,0,0,.6);
        }
        &#038;.active{
          opacity: .7;
        }
      }
    }
  }
  </pre>


<p>
  JS-код:
</p>


<pre>
  $(function() {

    // Инициализация слайдера
    $('.jcarousel').jcarousel({
        // Базовые настройки скрипта пишутся здесь
    });

    // Прокрутка слайдера

    // Кнопка PREV
    $('.jcarousel-prev')
    // Триггер класса inactive
    .on('jcarouselcontrol:active', function() {
        $(this).removeClass('inactive');
    })
    .on('jcarouselcontrol:inactive', function() {
        $(this).addClass('inactive');
    })
    // Инициализация кнопки PREV
    .jcarouselControl({
        target: '-=1'
    });

    // Кнопка NEXT
    $('.jcarousel-next')
    // Триггер класса inactive
    .on('jcarouselcontrol:active', function() {
        $(this).removeClass('inactive');
    })
    .on('jcarouselcontrol:inactive', function() {
        $(this).addClass('inactive');
    })
    // Инициализация кнопки NEXT
    .jcarouselControl({
        target: '+=1'
    });

    // Пагинация слайдера
    $('.jcarousel-pagination')
    // Триггер класса active
    .on('jcarouselpagination:active', 'a', function() {
        $(this).addClass('active');
    })
    .on('jcarouselpagination:inactive', 'a', function() {
        $(this).removeClass('active');
    })
    // Инициализация пагинации
    .jcarouselPagination({
        item: function(page) {
            return '<a href="#' + page + '">' + page + '</a>';
        }
    });

    // Автопрокрутка слайдера
    $('.jcarousel').jcarouselAutoscroll({
        interval: 3000,
        target: '+=1',
        autostart: true
    });

  });
  </pre>


<p>
  На этом все &#8211; удачного кодинга!
</p>


<p>
  Оцените статью:<br />
    <span id="post-ratings-1366" class="post-ratings" data-nonce="f9226d64f7"><img id="rating_1366_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1366, 1, '1 Star');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1366_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1366, 2, '2 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1366_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1366, 3, '3 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1366_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1366, 4, '4 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1366_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1366, 5, '5 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>8</strong> votes, average: <strong>4,50</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1366_text"></span></span><span id="post-ratings-1366-loading" class="post-ratings-loading">
  			<img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>
</p>

 [1]: http://sorgalla.com/jcarousel/ "Jan Sorgalla"
 [2]: http://plugins.jquery.com/tag/carousel/ "jQuery Plugins"
 [3]: http://sorgalla.com/jcarousel/dist/ "jCarousel Dist"
 [4]: http://placehold.it "Placehold.it"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/06/jCarousel_prev-next.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/06/jCarousel_pagination.jpg
 [7]: http://sorgalla.com/jcarousel/examples/ "Examples"