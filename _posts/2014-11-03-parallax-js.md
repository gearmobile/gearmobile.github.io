---
title: "Parallax.js - создаем простой parallax"
layout: post
categories: javascript
tags: [parallax, javascript]
share: true
---

> Небольшой обзор новой для меня темы - создание эффекта `parallax` на странице сайта. Вместе с вами буду учиться создавать такой эффект и начну с самого простого - Parallax.js.

Чтобы посмотреть, что примерно мы должны в результате получить, посмотрим на домашнюю страницу этого проекта - [Parallax.js][1]. Исходный код скрипта и документация расположена на GitHub - [Parallax.js][2]

## Кратко о parallax

Что такое `parallax` как эффект сам по себе, хорошо видно на самой страничке и расписывать его я не буду. В Интернет есть лучшее и более подробное описание эффекта `parallax`. Единственное, что можно сказать по поводу `parallax` - появился он в основном как необходимость, дань моде. Своим существованием практически полностью обязан популярным на сегодняшний день `landing page` и призван скрасить и разнообразить их относительную монотонность.

Способов реализации `parallax` на сегодня сушествует множество. Но практически все они основаны на одном принципе - изменении скорости прокрутки фонового изображения на странице относительно других объектов на ней (*поправьте меня, если я неправ*).

Одним из преимуществ метода на основе скрипта Parallax.js является то, что в этом случае не требуется библиотеки jQuery. Скрипт может работать и с ней, но ее присутствие совсем необязательно. Получается выгода в весе страницы и скорости ее загрузки в браузере.

## Parallax.js - начальная разметка

HTML-разметка для нашего будущего `parallax` удивительно простая - это маркированный список `ul` с идентификатором (*имя его произвольное*) и элементами списка `li` (*имя класса обязательно и неизменно*).

Еще одним обязательным атрибутом для элементов списка `li` является атрибут `data-depth`, у которого значение может меняться в диапазоне от 0 до 1. Чем выше значение в 1, тем выше скорость перемещения объекта на странице.

Внутрь элементов списка помещается изображение, которое будет анимироваться с помощью эффекта `parallax`.

Ниже приведен пример такой разметки:

{% highlight html %}
<ul id="scene">
  <li class="layer" data-depth="0.10">
    <img src="images/one.png" height="100" width="100" alt="Image" />
  </li>
  <li class="layer" data-depth="0.80">
    <img src="images/two.png" height="100" width="100" alt="Image" />
  </li>
  <li class="layer" data-depth="0.20">
    <img src="images/three.png" height="100" width="100" alt="Image" />
  </li>
  <li class="layer" data-depth="0.80">
    <img src="images/four.png" height="100" width="100" alt="Image" />
  </li>
</ul>
{% endhighlight %}

## Parallax.js - стилизация parallax

Произведем небольшую стилизацию нашего будущего `parallax` с помощью Sass/Compass. Для элемента `ul` добавим фоновое изображение, чтобы был лучше виден эффект parallax.

{% highlight css %}
@import "compass/";
@import "compass/reset";

#scene{
  width: 95%;
  margin: 20px auto 0;
  min-height: 775px;
  background: url(../images/bg.jpg) 0 0 no-repeat;
  img{
    display: inline-block;
    width: 100px;
    height: 100px;
    @include border-radius(50%);
  }
  img[src="images/one.png"]{
    margin: 200px 0 0 200px;
  }
  img[src="images/two.png"]{
    margin: 200px 0 0 1000px;
  }
  img[src="images/three.png"]{
    margin: 500px 0 0 700px;
  }
  img[src="images/four.png"]{
    margin: 600px 0 0 300px;
  }
}
{% endhighlight %}

## Parallax.js - добавляем javascript

Наш `parallax` почти готов - осталось "вдохнуть в него жизнь" с помощью Javascript.

Тут все просто. Первой строкой подключается файл скрипта Parallax.js. Второй строкой сначала в теле документа отыскивается элемент с идентификатором `scene`, который помещается внутрь переменной `scene`. Затем создается новый экземпляр `parallax` объекта Parallax и ему передается в качестве аргумента эта переменная `scene`.

Все - смотрим результат:

![Готовый эффект на Parallax.js]({{site.url}}/images/uploads/2014/11/ParallaxJS.png)

Достаточно подвигать мышью над фотографией красавчика на заднем плане, чтобы увидеть, как разноцветные кружки перемещаются с разной скоростью.

Мы получили эффект parallax.

Ниже приведен полный код HTML и CSS рассмотренного нами примера:

{% highlight html %}
<ul id="scene">
  <li class="layer" data-depth="0.10">
    <img src="images/one.png" height="100" width="100" alt="Image"
  </li>
  <li class="layer" data-depth="0.80">
    <img src="images/two.png" height="100" width="100" alt="Image"
  </li>
  <li class="layer" data-depth="0.20">
    <img src="images/three.png" height="100" width="100" alt="Image"
  </li>
  <li class="layer" data-depth="0.80">
    <img src="images/four.png" height="100" width="100" alt="Image"
  </li>
</ul><!-- scripts -->
{% endhighlight %}

{% highlight css %}
@import "compass";
@import "compass/reset";

scene{
width: 95%;
 margin: 20px auto 0;
 min-height: 775px;
 background: url(../images/bg.jpg) 0 0 no-repeat;
 img{
 display: inline-block;
 width: 100px;
 height: 100px;
 @include border-radius(50%);
 }
 img[src="images/one.png"]{
 margin: 200px 0 0 200px;
 }
 img[src="images/two.png"]{
 margin: 200px 0 0 1000px;
 }
 img[src="images/three.png"]{
 margin: 500px 0 0 700px;
 }
 img[src="images/four.png"]{
 margin: 600px 0 0 300px;
 }
}
{% endhighlight %}

Полный исходный код примера можно посмотреть на GitHub - [Parallax.js][3]

---

[1]: http://matthew.wagerfield.com/parallax/ "Parallax.js"
[2]: https://github.com/wagerfield/parallax "Parallax.js"
[3]: https://github.com/gearmobile/zencoder/tree/master/parallaxjs "Parallax.js"
