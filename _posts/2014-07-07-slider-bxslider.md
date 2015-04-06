---
title: "Слайдер bxSlider"
layout: post
categories: javascript
tags: [bxslider, javascript]
share: true
---

> Обзор еще одного слайдера под библиотеку jQuery под названием bxSlider.

Данный слайдер обладает полным набором возможностей, адаптивный и легко устанавливается в проекте. Адрес проживания слайдера bxSlider - [The Responsive jQuery Content Slider][1].

Конкретно какими возможностями обладает bxSlider:

  * полностью адаптивный
  * может быть горизонтальным, вертикальным
  * может содержать в себе изображения, видео или HTML-контент
  * поддержка функций touch/swipe
  * для анимаций используются CSS transitions
  * маленький размер файла, легко видоизменяется и настраивается
  * поддержка браузерами Firefox, Chrome, Safari, iOS, Android, Ie7+
  * большое число настроек

## Установка слайдера bxSlider

Установка bxSlider ничем не отличается от установки ему подобных скриптов для создания carousel. Скачиваем с сайта архив - в нем есть все необходимое для подключения и работы. Помимо этого, там есть несколько дополнительных файлов типа `jquery.easing.1.3.js` и `jquery.fitvids.js`. Но нет библиотеки jQuery, которую автор рекомендует подключать в проект через CDN. Я подключу jQuery локально, версии 1.11.1.

В HTML-файле перед закрывающим тегом body произвожу подключение скриптов в таком порядке:

{% highlight html %}
...
<!--  SCRIPTS  -->
<script src="js/jquery-1.11.1.min.js"></script>
<script src="js/jquery.bxslider.min.js"></script>
<script src="js/bxslider.js"></script>
{% endhighlight %}

Файл `jquery.bxslider.min.js` беру из скачанного архива, файл `bxslider.js` - произвольного имени, для настроек плагина bxSlider.

В `head` HTML-документа, помимо этого, производится подключение таблицы стилей для плагина bxSlider, которую также беру из скачанного архива. Данный шаг выполнять совершенно необязательно - можно обойтись без файла `jquery.bxslider.css` и тогда получим "чистый" слайдер, который можно видоизменять по своему с помощью CSS:

{% highlight html %}
<head>
  <meta charset="utf-8">
  <title>Document</title>
  <link rel="stylesheet" href="css/jquery.bxslider.css">
  ...
 </head>
{% endhighlight %}

Плагин bxSlider подключен и готов к работе. Осталось создать HTML-разметку для него.

## HTML-разметка для слайдера bxSlider

Внутри тега `body` создаю разметку для будущего слайдера. Она проста и семантична, представляет из себя обычный маркированный список, в котором каждый элемент `li` является слайдом. Внутри `li` может размещаться изображение, видео или любой другой HTML-контент. Контейнер `ul` должен иметь класс с произвольным именем:

{% highlight html %}
<ul class="slider">
  <li><img src="http://placehold.it/300x200" alt="bxSlider" /></li>
  <li><img src="http://placehold.it/300x200" alt="bxSlider" /></li>
  <li><img src="http://placehold.it/300x200" alt="bxSlider" /></li>
  <li><img src="http://placehold.it/300x200" alt="bxSlider" /></li>
</ul>
{% endhighlight %}

## Инициализация скрипта bxSlider

В созданном ранее js-файле `bxslider.js` произвожу инициализацию плагина bxSlider. Важно заметить, что строка инициализации должна быть обязательно заключена в "обертку" `$(document).ready()`, иначе слайдер не будет работать:

{% highlight javascript %}
$(document).ready(function(){
  $('.slider').bxSlider();
});
{% endhighlight %}

Смотрю готовый результат:

![Запущенный слайдер bxSlider]({{site.url}}/images/uploads/2014/07/bxslider_ready.png)

Слайдер bxSlider запущен и работает - есть кнопки пагинации и перемотки, изображения крутятся при нажатии на них. Пробую отключить таблицу стилей `jquery.bxslider.css` и смотрю результат. Действительно, слайдер bxSlider получается "голым", но рабочим:

![Чистый слайдер bxSlider]({{site.url}}/images/uploads/2014/07/bxslider_clean.png)

## Стилизация слайдера bxSlider

Произведу небольшую стилизацию слайдера bxSlider. Для этого необходимо воспользоваться плагином Firebug под браузер Mozilla Firefox, чтобы инспектировать DOM-дерево и находить нужные HTML-элементы с их классами. Как можно было понять из базовой HTML-разметки, все элеметы управления слайдером генерируются скриптом автоматически.

Стилизация слайдера bxSlider с помощью CSS-правил (в данном примере это SCSS) может быть такой:

{% highlight css %}
$asidePos: 50px;
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
    &:hover,&:focus{
      outline: none;
      background-color: darken($color,5%);
    }
    &:active{
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
{% endhighlight %}

И посмотрим результат наших трудов. Уже гораздо лучше, однако:

![Стилизованный слайдер bxSlider]({{site.url}}/images/uploads/2014/07/bxslider_styled.png)

## Настройка слайдера bxSlider

Плагин bxSlider имеет большое количество настроек, которые легко подключать в коде. Разнообразные (и многочисленные) примеры создания слайдера приведены на странице - [Examples][2]. Эти примеры можно и стоит изучить (*хотя бы слегка, для будущего*).

В этой статье давайте я воссоздам один из приведенных на странице [Examples][2] примеров. Пусть это будет слайдер с автоматической прокруткой и кнопками управления прокруткой - запуско и остановкой. Такой готовый пример размещен здесь - [Auto show with start / stop controls][3]. Я просто сделаю свой собственный дубликат, со своими стилями.

Для этого в SCSS-коде добавляю такие строки:

{% highlight css %}
/*  auto controls  */
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
{% endhighlight %}

HTML-разметку на странице я не меняю, как вы могли заметить. Блок `.bx-controls-auto` генерируется скриптом bxSlider автоматически.

Файл настроек `bxslider.js` подправляю, чтобы он выглядел таким образом:

{% highlight css %}
$(document).ready(function(){
  $('.slider').bxSlider({
    auto: true,
    autoControls: true
  });
});
{% endhighlight %}

Смотрю результат в браузере:

![Слайдер bxSlider с автоматической прокруткой]({{site.url}}/images/uploads/2014/07/bxslider_autoplay.png)

Отлично! Появились кнопки запуска и остановки показа слайдшоу; сам слайдер стартует автоматически, при открытии страницы в окне браузера.

## Заключение

Плагин bxSlider мне однозначно понравился. Семнатичная простая разметка, использование произвольного имени класса (а не идентификатора), автоматическое генерирование HTML-элементов слайдера, большое количество настроек, хорошие эффекты, простота подключения.

Все эти преимущества однозначно сделали плагин bxSlider номером один в моей копилке.

---

 [1]: http://bxslider.com/ "The Responsive jQuery Content Slider"
 [2]: http://bxslider.com/examples "Examples"
 [3]: http://bxslider.com/examples/auto-show-start-stop-controls "Auto show with start / stop controls"
