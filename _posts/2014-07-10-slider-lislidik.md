---
title: "Слайдер liSlidik"
layout: post
categories: javascript
tags: [jquery, lislidik]
share: true
---

> На моем пути повстречался еще один плагин для создания карусели (carousel), основанный на библиотеке jQuery.

Имя этого плагина запоминающиеся - liSlidik и проживает он здесь - [liSlidik - jQuery Responsive Slider][1]. Насколько я правильно понял, этот плагин был создан одним или несколькими русскоязычными веб-разработчиками. В принципе, вся документация с примерами подробно расписана на русском языке на этой странице и нет нужды пересказывать уже сказанное.

Однако, я хотел разобраться с плагином liSlidik - понять, как его подключать, настраивать и управлять. Поэтому все же появился обзор этого слайдера, который будет представлен ниже.

Сразу скажу, что плагин liSlidik мне не понравился. На это есть несколько причин, которые я укажу ниже, в самом обзоре. Причины эти могут быть субъективными, но все же они повлияли на мой вывод.

## Установка плагина liSlidik

Установка и подключение плагина liSlidik производится совершенно стандартно для скриптов подобного рода. Сначала подключается библиотека jQuery (в этом обзоре использовалась версия 1.8), затем подключается сам скрипт liSlidik, а в конце - js-файл с инициализацией скрипта и его настройками:

<pre></pre>

Скачать архив скрипта liSlidik можно с домашней страницы проекта по это ссылке - [liSlidik Download][2]. Помимо этого, на jsFiddle выложен исходный код скрипта с примерами создания разных вариантов слайдов - [liSlidik Demo][3]. Библиотеку jQuery можно подключить через CDN или скачать для локального подключения - это кому как нравиться.

## HTML-разметка для liSlidik

Разметка в HTML-документе для будущего слайдера под управлением скрипта liSlidik проста и семантична - в этом плане все на уровне современной веб-разработки. Структура будущего слайдера представляет из себя обычный маркированный список с вложенными изображениями:

{% highlight html %}
<ul id="slider" class="slider">
  <li><img src="http://placehold.it/300x200&text=liSlidik 1" alt="liSlidik 0" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 2" alt="liSlidik 1" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 3" alt="liSlidik 2" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 4" alt="liSlidik 3" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 5" alt="liSlidik 4" /></li>
</ul>
{% endhighlight %}

Единственный важный момент при создании HTML-разметки заключается в том, что для элемента `ul` необходимо задать идентификатор, к которому будет "цепляться" скрипт liSlidik - иначе слайдер не заработает (*мне этот факт не понравился, так как я не люблю идентификаторы и стараюсь всячески избегать их использования*). Класс для элемента `ul` понадобиться для последующей стилизации слайдера на HTML-странице.

## Инициализация скрипта liSlidik

Для "запуска" скрипта liSlidik нужно его инициализировать, создав простой js-файл и прописав в нем такие строки:

{% highlight javascript %}
$(document).ready(function(){
  $('#slider').liSlidik();
});
{% endhighlight %}

## Минимальная стилизация скрипта liSlidik

Слайдер liSlidik после всех выполненных выше мною шагов не заработает, на самом деле. Потому что для его работы необходима минимальная CSS-стилизация, которую я выполню ниже. Стоит ли говорить, что данный шаг я бы не смог выполнить без незаменимого плагина Firebug под Mozilla Firefox?!

Минимальная CSS-стилизация слайдера liSlidik:

{% highlight css %}
.slider{
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
{% endhighlight %}

Конечно, можно воспользоваться готовыми CSS-стилями из архива скрипта liSlidik; но зачем пользоваться чужим кодом, когда можно создать более чистый и маленький по размеру свой собственный код, мне не понятно. Конечно, в приведенном выше коде значения свойств `width` и `height` являются произвольными и зависят от конкретных условий - ставить нужно вместо них то, что необходимо. Это же относится и к `margin: 20px auto;`, которое было применено здесь для "красоты".

Вот теперь слайдер liSlidik готов к работе. Более того - он работает! Это минималистичный слайдер, без каких-либо кнопок управления:

![Скрипт liSlidik работает]({{site.url}}/images/uploads/2014/07/lislidik_clean.png)

## Кнопки управления для liSlidik

Скрипт liSlidik имеет в своем составе полный набор органов управления создаваемым им слайдером. Начну с малого и приступлю к созданию кнопок перемотки взад-вперед для слайдшоу. Стоит сразу сказать, что все органы управления показом слайдшоу в скрипте liSlidik не создаются автоматически - их нужно создавать вручную (*данный факт мне также не совсем понравился*):

{% highlight html %}
<!--  arrows  -->
<a data-slidik="slider" class="next" href="#">Next</a>
<a data-slidik="slider" class="prev" href="#">Prev</a>
{% endhighlight %}

HTML-разметка для кнопок перемотки создается через элемент `a`, у которого обязательным атрибутом должен быть `data-slidik="slider"`, где `slider` - это имя идентификатора нашего слайдера. Классы `class="next"` и `class="prev"` присутствуют для тех же целей, что и в элементе `ul` - на них "вешаются" CSS-стили:

{% highlight css %}
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
  &:hover,&:focus{
    background-color: lighten(#000,20%);
  }
}
.prev{
  right: 10px;
  &:hover,&:focus{
    background-color: lighten(#000,20%);
  }
}
{% endhighlight %}

Смотрим результат подключения кнопок перемотки в liSlidik:

![Плагин liSlidik c кнопками перемотки]({{site.url}}/images/uploads/2014/07/lislidik_arrows.png)

## Пагинация в слайдере liSlidik

Подключение пагинации в скрипте liSlidik выполняется аналогично - нужно вручную создать блочный элемент `div` с атрибутом `data-slidik="slider"` и классом `class="dotted"` (который также обязателен в данном случае!):

{% highlight html %}
<!--  pagination  -->
<div data-slidik="slider" class="dotted">
</div>
{% endhighlight %}

Создаю для нового элемента CSS-стили. Снова оговорюсь, что для блока пагинации (*насколько я правильно понял*) имя класса `dotted` является обязательным. Я пробовал менять это имя на произвольное и в результате слайдер перестал работать (*вот такие мелкие обязательства мне и не нравятся в этом плагине!*):

{% highlight css %}
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
    &:hover,&:focus{
      background-color: lighten(#000,40%);
    }
    &.cur{
      background-color: lighten(#000,50%);
    }
  }
}
{% endhighlight %}

Присутствующее в коде выше имя класса `.cur` обозначает активный элемент, который можно стилизовать на свой выбор. Еще один странный момент, связанный со слайдером liSlidik - внимательно посмотрите на снимок работающего скрипта:

![Скрипт liSlidik c пагинацией]({{site.url}}/images/uploads/2014/07/lislidik_pagination.png)

Ничего не замечаете? Нумерация в данной пагинации начинается с нуля! Это весьма странный факт, ибо обычные посетители сайта не являются программистами и для них нумерация с нуля, мягко выражаясь, непривычна и необычна.

## Заголовок слайдера liSlidik

Заголовок для слайдера liSlidik создается вручную (*неужели нельзя создать скрипт, который автоматически генерирует нужные HTML-элементы?*) также с помощью блочного элемента `div`, для которого прописывается атрибут `data-slidik="slider"` с обязательным именем класса `class="caption"`:

{% highlight html %}
<!--  caption  -->
<div data-slidik="slider" class="caption"></div>
{% endhighlight %}

И произвольные CSS-стили для него:

{% highlight css %}
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
{% endhighlight %}

Текст для показа на странице скрипт liSlidik берет из содержимого атрибута `alt=` для элемента `img`. Поэтому не забудьте его прописать в своей HTML-разметке!

![Скрипт liSlidik c заголовком]({{site.url}}/images/uploads/2014/07/lislidik_caption.png)

## Миниатюры в скрипте liSlidik

Плагин liSlidik имеет возможность создания миниатюр в виде галлереи изображений, которая выступает в роли пагинации. На странице демо-примеров показан вариант такого слайдшоу. Однако, у меня не было желания разбираться с вопросом построения `thumnnails` в этом примере.

## Заключение

Все примеры и варианты создания слайдеров под управлением скрипта liSlidik можно посмотреть на официальной страничке проекта - [liSlidik - jQuery Responsive Slider][1]. Ниже привожу полный HTML и SCSS-код примера, рассмотренного в данной статье:

{% highlight html %}
<ul id="slider" class="slider">
  <li class="show"><img src="http://placehold.it/300x200&text=liSlidik 1" alt="liSlidik 0" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 2" alt="liSlidik 1" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 3" alt="liSlidik 2" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 4" alt="liSlidik 3" /></li>
  <li><img src="http://placehold.it/300x200&text=liSlidik 5" alt="liSlidik 4" /></li>
  <!--  arrows  -->
  <a data-slidik="slider" class="next" href="#">Next</a>
  <a data-slidik="slider" class="prev" href="#">Prev</a>
  <!--  pagination  -->
  <div data-slidik="slider" class="dotted"></div>
  <!--  caption  -->
  <div data-slidik="slider" class="caption"></div>
  <!--  previews  -->
  <!-- <div data-slidik="slider" class="thumbs"></div> -->
</ul><!--  SCRIPTS  -->
{% endhighlight %}

{% highlight css %}
.slider{
  width: 300px;
  height: 200px;
  margin: 20px auto;
  position: relative;
  li{
    border: 2px solid #000;
    position: absolute;
    top: -2px;
    left: -2px;
    &.show{
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
    &:hover,&:focus{
      background-color: lighten(#000,20%);
    }
  }
  .prev{
    right: 10px;
    &:hover,&:focus{
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
      &:hover,&:focus{
        background-color: lighten(#000,40%);
      }
      &.cur{
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
{% endhighlight %}

---

 [1]: http://masscode.ru/index.php/k2/item/46-lislidik "liSlidik - jQuery Responsive Slider"
 [2]: http://masscode.ru/files/zip/liSlidik.zip "liSlidik Download"
 [3]: http://jsfiddle.net/yurik417/R5jB6/8/ "liSlidik Demo"
