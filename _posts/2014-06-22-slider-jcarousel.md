---
title: "Слайдер jCarousel"
layout: post
categories:
tags: [jCarousel, javascript]
share: true
---

> Данная статья посвящена обзору еще одного js-плагина для создания `slideshow` из картинок - jCarousel.

Автором данного скрипта является [Jan Sorgalla][1]. Хотя мне эти имя и фамилия ни о чем не говорит, но они запоминающиеся. Название данного плагина я запомнил по имени его автора раньше, чем по имени самого скрипта.

Скрипт jCarousel по популярности в списке плагинов типа `carousel` занимает второе место после скрипта slick - [jQuery Plugins][2]. Кто вдруг не знает, термин `carousel` (карусель) является общим описанием плагинов и скриптов подобного типа.

Плагин jCarousel основан на библиотеке jQuery и предоставляет стандартные возможности управления показом картинок - кнопки перемотки взад-вперед и пагинация картинок. Показ заголовка картинки не предусмотрен, но имеется возможность автоскроллинга изображений.

## Особенности jCarousel

Первая особенность плагина заключается в том, что здесь почти ничего не генерируется автоматически, самим скриптом jCarousel. Только пагинация создается с помощью js-кода, все остальное нужно прописывать вручную в HTML-коде. Для меня это было весьма огорчительно, так как такой подход занимает много времени и сил.

Вторая особенность плагина - он имеет модульную структуру. То есть, имеется основная составляющая скрипта jCarousel - `jquery.jcarousel-core.min.js`, которая на то и является основной, что предоставляет базовые возможности для создания слайдшоу.

Если необходимо к слайдшоу добавить возможность прокрутки, то нужно скачать и подключить модуль `jquery.jcarousel-control.min.js`. Для включения возможности пагинации необходим еще один модуль - `jquery.jcarousel-pagination.min.js`.

Для автоскролинга потребуется модуль `jquery.jcarousel-autoscroll.min.js`.

В проекте перечисленные выше модули подключаются последовательно, в таком порядке (первые два пункта строго обязательны, остальные могут добавляться, убираться и перемещаться между собой произвольно):

* библиотека jQuery - `jquery-1.11.1.min.js`
* основной модуль jCarousel Core - `jquery.jcarousel-core.min.js`
* модуль прокрутки - `jquery.jcarousel-control.min.js`
* модуль пагинации - `jquery.jcarousel-pagination.min.js`
* модуль автоскроллинга - `jquery.jcarousel-autoscroll.min.js`

Справедливости стоит сказать, что можно не заморачиваться с отдельными модулями и подключить все одним файлом, по типу "все включено" - `jquery.jcarousel.min.js`:

* библиотека jQuery - `jquery-1.11.1.min.js`
* плагин jCarousel со всеми его возможностями - `jquery.jcarousel.min.js`

Страница для скачивания плагина jCarousel одним файлом (Full Download) или отдельными его модулями (Separate Downloads) расположена здесь - [jCarousel Dist][3]. Можно получить как "Production Version" (compressed), так и "Development Version" (uncompressed).

В данной статье будут использоваться сжатые версии скрипта, так как в исходном коде плагина копаться не будем.

Плагин требует для своей работы библиотеку jQuery **версии не ниже 1.7** - это также стоит учесть.

## Подключение плагина jCarousel

Создаем набросок HTML-страницы и производим подключение плагина jCarousel. Для чистоты и наглядности буду применять подход модульности плагина. Как и любой другой плагин подобного рода, его управление производится через отдельный js-файл произвольного имени, в котором прописываются параметры скрипта. Я создал для этой цели js-файл `simple.js` и выполнил подключение таким образом:

<pre></pre>

Шкурка `style.css` служит для стилизации слайдера jCarousel на HTML-странице, то есть в этом файле будут писаться CSS-стили для всех элементов слайдера jCarousel.

## Базовая разметка слайдера jCarousel

Плагин для своей работы требует некоторую обязательную базовую HTML-разметку и CSS-стили к ней. HTML-разметка может быть не обязательно именно такой, как представлена ниже, но основная ее структура должна сохраняться:

{% highlight html %}
<div class="jcarousel">
  <ul>
    <li>
      <img src="http://placehold.it/600x400/778899/fff&text=Slide 1" alt="" />
    </li>
    <li>
      <img src="http://placehold.it/600x400/778899/fff&text=Slide 2" alt="" />
    </li>
    <li>
      <img src="http://placehold.it/600x400/778899/fff&text=Slide 3" alt="" />
    </li>
    <li>
      <img src="http://placehold.it/600x400/778899/fff&text=Slide 4" alt="" />
    </li>
    <li>
      <img src="http://placehold.it/600x400/778899/fff&text=Slide 5" alt="" />
    </li>
    <li>
      <img src="http://placehold.it/600x400/778899/fff&text=Slide 6" alt="" />
    </li>
  </ul>
</div>
<!--  end jcarousel  -->
{% endhighlight %}

То есть, должен присутствовать блок-обертка с классом `class="jcarousel"` (имя класса может быть произвольным), внутри которого должен находиться еще один блок-обертка. И затем только идут элементы с картинками. HTML-структура, надо сказать, несколько громоздкая по стандартам сегодняшнего времени.

К обязательной базовой HTML-разметке "прилагаются" не менее обязательные CSS-стили:

{% highlight javascript %}
.jcarousel {
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
{% endhighlight %}

Код выше - это конечно не совсем CSS-код. Это SCSS, но наглядность (как мне кажется) от этого только выигрывает из-за ярко выраженного nesting, присущего Sass. По крайней мере, ничего не стоит за 5-10 секунд вручную перевести этот SCSS в обычный CSS, если кого вдруг это не устраивает.

В данном примере я воспользовался сервисом [Placehold.it][4] для быстрой и удобной генерации картинок в создаваемом слайдшоу.

Для активации слайдера в файле настроек `simple.js` скрипта jCarousel нужно прописать его инициализацию:

{% highlight javascript %}
$(function() {
  // Инициализация слайдера
  $('.jcarousel').jcarousel({
    // Базовые настройки скрипта пишутся здесь
  });
});
{% endhighlight %}

Слайдер уже готов! Правда, увидеть его работу не получиться, так как не заданы настройки скрипта, не созданы элементы для его управления. Приступим к созданию элементов управления слайдера jCarousel.

## Создание кнопок прокрутки в jCarousel

Как я уже упоминал ранее, при создании слайдера придется все создавать вручную, прописывая нужные HTML-элементы внутри HTML-документа.

Какой уважающий себя слайдер картинок может существовать без кнопок перемотки изображений взад-вперед? Конечно - никакой! Поэтому потребуется их создать.

Для этого ниже блока со слайдером дописываю две ссылки с классами `class="jcarousel-prev"` и `class="jcarousel-prev"`:

{% highlight javascript %}
<div class="wrap_jcarousel">
  <div class="jcarousel">
    <ul>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 1" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 2" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 3" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 4" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 5" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 6" alt="" />
      </li>
    </ul>
  </div>
  <!--  end jcarousel  -->
  <!--  CONTROLS  -->
  <a class="jcarousel-prev" href="#">Prev</a>
  <a class="jcarousel-next" href="#">Next</a>
</div>
<!--  end wrap_jcarousel  -->
{% endhighlight %}

Блок слайдера, элементы прокрутки (и другие будущие элементы управления слайдером) я поместил внутрь одного общего блока-обертки `class="wrap_jcarousel"`, которому придал несложные CSS-стили:

{% highlight javascript %}
.wrap_jcarousel{
  width: 600px;
  margin: 10px auto;
  position: relative;
{% endhighlight %}

Кнопки перемотки внутри HTML-разметки созданы, однако необходимо прикрутить к ним действия с помощью js-скрипта. Для этого сначала подключаю модуль прокрутки `jquery.jcarousel-control.min.js` в HTML-документе:

<pre></pre>

... а затем в файле настроек `simple.js` активирую возможность прокрутки слайдера, добавив базовые js-строки:

{% highlight javascript %}
$(function() {
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
{% endhighlight %}

После стилизации элементов управления и блока-обертки `class="wrap_jcarousel"` слайдер jCarousel может принять следующий вид:

![Слайдер jCarousel с кнопками прокрутки]({{site.url}}/images/uploads/2014/06/jCarousel_prev-next.jpg)

Попробуем прокрутить картинки взад и вперед с помощью кнопок - все работает!

## Добавление пагинации в jCarousel

Для добавления пагинации в слайдере нужно создать в HTML-разметке дополнительный блок с классом `class="jcarousel-pagination"`:

{% highlight html %}
<div class="wrap_jcarousel">
  <div class="jcarousel">
    <ul>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 1" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 2" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 3" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 4" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 5" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 6" alt="" />
      </li>
    </ul>
  </div>
  <!--  end jcarousel  -->
  <!--  CONTROLS  -->
  <a class="jcarousel-prev" href="#">Prev</a>
  <a class="jcarousel-next" href="#">Next</a>
  <!--  PAGINATION  -->
  <p class="jcarousel-pagination"></p>
</div>
<!--  end wrap_jcarousel  -->
{% endhighlight %}

Больше ничего в него добавлять не нужно - плагин сам сгенерирует (*наконец-то сам что создаст!*) его содержимое. Нам только необходимо подключить соответствующий модуль `jquery.jcarousel-pagination.min.js` для пагинации в слайдере:

<pre></pre>

... а затем активировать его в файле настроек `simple.js`:

{% highlight javascript %}
$(function() {

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
{% endhighlight %}

Для стилизации пагинации с данном случае потребуется плагин Firebug под Mozilla Firefox для инспекции генерируемых скриптом jCarousel элементов. Примерный вид слайдера после применения некоторых CSS-стилей может быть таким:

![Слайдер jCarousel с пагинацией]({{site.url}}/images/uploads/2014/06/jCarousel_pagination.jpg)

Проверим работу пагинации и "пощелкаем" на кнопках с циферками - все работает!

## Добавление автопрокрутки в jCarousel

Для автоматической прокрутки изображений в слайдере достаточно выполнить два несложных действия, которые выполнялись и ранее.

Первое - подключить модуль автопрокрутки `jquery.jcarousel-autoscroll.min.js`:

<pre></pre>

Второе - активировать автопрокрутку в файле настроек `simple.js`:

{% highlight javascript %}
$(function() {

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
{% endhighlight %}

Перезапускаю браузер, в котором открыт создаваемый мною слайдер и любуюсь результатом.

## Дополнительные украшательства для jCarousel

Что еще можно сделать для созданного слайдера jCarousel? Можно добавить стили для неактивной кнопки прокрутки изображений и для активной кнопки пагинации. Активность и неактивность этих кнопок можно отслеживать в помощью js-строк и "вешать" на нужные состояния кнопок соответствующие CSS-классы.

Для этого файл `simple.js` преобразую таким образом:

{% highlight javascript %}
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
{% endhighlight %}

... а в `style.scss` добавлю строки:

{% highlight javascript %}
/*  PREV NEXT BUTTONS  */
.jcarousel-prev,
.jcarousel-next{
  position: absolute;
  top: 200px;
  ...
  &.inactive{
    cursor: default;
  }
}
...
/*  PAGINATION  */
.jcarousel-pagination{
  background-color: transparent;
  position: absolute;
  ...
    &.active{
      opacity: .7;
    }
  }
{% endhighlight %}

Теперь при автоматической прокрутке изображений активная кнопка пагинации будет выделяться цветом. А при достижении конца прокрутки кнопка прокрутки становится неактивной, что визуально отмечается изменением вида курсора мыши при его наведении на кнопку.

## Заключение jCarousel

В заключение можно сказать, что на странице примеров [Examples][7] есть богатый материал для дополнительных экспериментов. В частности, интерес представляет адаптивная Responsive Carousel, которая изменяет количество картинок внутри блока в зависимости от ширины окна браузера.

Полный код рассмотренного в данной статье примера создания слайдера приведен ниже.

{% highlight html %}
<div class="wrap_jcarousel">
  <div class="jcarousel">
    <ul>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 1" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 2" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 3" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 4" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 5" alt="" />
      </li>
      <li>
        <img src="http://placehold.it/600x400/778899/fff&text=Slide 6" alt="" />
      </li>
    </ul>
  </div>
  <!--  end jcarousel  -->
  <!--  CONTROLS  -->
  <a class="jcarousel-prev" href="#">Prev</a>
  <a class="jcarousel-next" href="#">Next</a>
      <!--  PAGINATION  -->
  <p class="jcarousel-pagination"></p>
</div>
<!--  end wrap_jcarousel  -->
{% endhighlight %}

{% highlight css %}
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
    &:hover{
      background-color: darken(#778899,10%);
    }
    &.inactive{
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
      &:first-child{
        margin-left: 0;
      }
      &:hover{
        background-color: rgba(0,0,0,.6);
      }
      &.active{
        opacity: .7;
      }
    }
  }
}
{% endhighlight %}



{% highlight javascript %}
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
{% endhighlight %}

На этом все - удачного кодинга!

---

 [1]: http://sorgalla.com/jcarousel/ "Jan Sorgalla"
 [2]: http://plugins.jquery.com/tag/carousel/ "jQuery Plugins"
 [3]: http://sorgalla.com/jcarousel/dist/ "jCarousel Dist"
 [4]: http://placehold.it "Placehold.it"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/06/jCarousel_prev-next.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/06/jCarousel_pagination.jpg
 [7]: http://sorgalla.com/jcarousel/examples/ "Examples"