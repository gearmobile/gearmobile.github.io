---
title: Слайдер jqFancyTransitions
layout: post
categories:
tags: [jqFancyTransitions, javascript]
share: true
---

> Данная статья посвящена обзору слайдера jqFancyTransitions - его установке, настройке и стилизации.

Слайдер jqFancyTransitions основан на библиотеке jQuery (впрочем, как и подавляющее большинство слайдеров подобного типа). Эффекты, применимые к данному слайдеру, можно посмотреть на домашней странице проекта - [jqFancyTransitions][1].

Их достаточное количество - `wave`, `zipper`, `curtain`, `curtain alternate`, `fountain top`, `random top`, `left top`, `right bottom`. Слайдер jqFancyTransitions предоставляет стандартный набор органов управления слайдшоу - кнопки перемотки взад-вперед, пагинация и показ заголовка картинки.

Помимо этого имеется возможность сделать изображения в слайдере ссылками.

## Установка jqFancyTransitions

Для подключения слайдера jqFancyTransitions в рабочий проект необходимо выполнить стандартные операции:

* подключить библиотеку jQuery
* подключить плагин jqFancyTransitions

<pre></pre>

В данной статье проверялась совместная работа плагина jqFancyTransitions с библиотекой jQuery версии 1.10.1. Другие версии jQuery не "испытывались", поэтому о их работоспособности с этим плагином ничего сказать не могу.

Естественно, подключать jQuery можно разными путями - локально или через разнообразные CDN, это уж кому как нравиться.

Затем создаем разметку для слайдера jqFancyTransitions в HTML-документе:

{% highlight html %}
<div id="slider">
  <img src="http://placehold.it/400x300/c8c8c8/fff" alt="Mascot 1" />
  <img src="http://placehold.it/400x300/b8b8b8/fff" alt="Mascot 2" />
  <img src="http://placehold.it/400x300/a8a8a8/fff" alt="Mascot 3" />
  <img src="http://placehold.it/400x300/989898/fff" alt="Mascot 4" />
  <img src="http://placehold.it/400x300/888888/fff" alt="Mascot 5" />
  <img src="http://placehold.it/400x300/787878/fff" alt="Mascot 6" />
</div>
{% endhighlight %}

Как видим, разметка чрезвычайно минималистична - блок-обертка с обязательным идентификатором `id` (если использовать класс вместо идентификатора, плагин jqFancyTransitions работать не будет) и набор изображений `img`.

В данном примере я воспользовался сервисом [Placehold.it][2] для быстрого и удобного способа эмуляции картинок в проекте.

Минималистичность HTML-разметки для работы плагина jqFancyTransitions - с точки зрения HTML-семантики просто прекрасно; а вот с точки зрения web-разработчика - не очень, так как придется в дальнейшем воспользоваться плагином [Firebug][3] под Mozilla Firefox, чтобы решить проблему стилизации слайдера jqFancyTransitions.

## Настройка jqFancyTransitions

Как любой слайдер подобного рода, jqFancyTransitions имеет набор опций для настройки своей работы. Можно управлять скоростью показа картинок, выбрать нужный эффект перехода, отобразить или скрыть элементы управления slideshow.

Полный список настроек представлен ниже:

{% highlight powershell %}
effect: '', // wave, zipper, curtain ( волны, застежка, занавес)
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
{% endhighlight %}

Настройка плагина jqFancyTransitions производится в отдельном js-файле с произвольным именем, который также подключается в проект после библиотеки jQuery и плагина jqFancyTransitions.

В моем случае я создал js-файл с именем script:

<pre></pre>

... и наполнил его первоначальным содержимым:

{% highlight javascript %}
$(document).ready(function(){
    $('#slider').jqFancyTransitions({
      width: 400,
      height: 300,
      navigation: true
    });
});
{% endhighlight %}

То есть, я задал для обертки с идентификатором `#slider` высоту и ширину через параметры `height: 300`, `width: 400`; также задал, что данный слайдер должен иметь органы управления - пагинацию и кнопки перемотки слайдшоу - `navigation: true`.

Отлично! Уже сейчас наш плагин должен работать:

![Слайдер jqFancyTransitions - первый запуск]({{site.url}}/images/uploads/2014/06/jqFancyTransitions_first-view.jpg)

Видим, что плагин jqFancyTransitions создал слайдшоу из шести картинок размером `400x300px`, как я и прописывал в HTML-разметке.

Помимо этого, плагином были сгенерированы кнопки перемотки взад-вперед (`prev` и `next`), пагинация (номера `1,2,3,4,5,6` внизу слайдера) и заголовок изображения (`title`).

Теперь осталось привести наш слайдер к тому виду, который необходим. В данном конкретном случае мне необходимо убрать кнопки перемотки, заголовок изображений; кнопки пагинации стилизовать и переместить вовнутрь слайдера. Этим я и займусь в следующей части данного обзора.

## Стилизация jqFancyTransitions

Для придания слайдеру jqFancyTransitions необходимого внешнего вида я воспользуюсь своим любимым Sass/Compass. Также для задачи стилизации слайдера потребуется плагин Firebug - незаменимая штука для web-разработчика.

В моем случае этот плагин понадобиться для определения имен идентификаторов и классов HTML-элементов, которые генерирует плагин jqFancyTransitions.

Чтобы было понятно, о чем идет речь, давайте взглянем на снимок окна браузера с запущенным плагином Firebug, который я сделал для данного примера. Посмотрим на вкладку HTML - там есть элементы, которые первоначально не присутствуют в нашей HTML-разметке:

![Слайдер jqFancyTransitions под прицелом Firebug]({{site.url}}/images/uploads/2014/06/jqFancyTransitions_Firebug.jpg)

Убираю кнопки перемотки и заголовок изображения. Для этого с помощью Firebug нахожу имена идентификаторов этих элементов и прописываю для них правила:

{% highlight css %}
#ft-prev-slider,
#ft-next-slider,
#ft-title-slider {
  display: none;
}
{% endhighlight %}

Пагинацию изображений `#ft-buttons-slider` перемещаю вверх и влево:

{% highlight css %}
#ft-buttons-slider{
  position: relative;
  top: -40px;
  right: 5px;
  padding-top: 0 !important;
  ...
{% endhighlight %}

Здесь стоит обратить внимание на последнее правило обнуления верхнего `padding` - для него потребовалось суровая мера в виде `!important`, чтобы переопределить внутренние стили, задаваемые самим плагином jqFancyTransitions для данного HTML-элемента.

Для кнопок пагинации `.ft-button-slider` задаю размер, фоновую заливку и расстояние между ними:

{% highlight css %}
.ft-button-slider{
  text-decoration: none;
  font-size: 12px;
  color: darken(#fff,10%);
  background-color: $color;
  margin-left: 10px;
  @include text-shadow(rgba(0,0,0,.5) 1px 1px 0);
{% endhighlight %}

Чтобы выделить активную кнопку в пагинации, создаю для генерируемого плагином jqFancyTransitions класса `.ft-button-slider-active` правила:

{% highlight css %}
.ft-button-slider-active{
  background-color: darken($color,10%);
  color: #fff;
}
{% endhighlight %}

Начиная с версии 1.7 плагин jqFancyTransitions позволяет создавать из изображений слайдера ссылки. То есть, картинки, мелькающие в виде `slideshow`, одновременно являются ссылками.

Чтобы сделать так, достаточно в HTML-разметке дописать теги ссылок:

{% highlight html %}
<div id="slider">
  <img src="http://placehold.it/400x300/c8c8c8/fff" alt="Mascot 1" />
    <a href="http://localhost:7788/third/"></a>
  <img src="http://placehold.it/400x300/b8b8b8/fff" alt="Mascot 2" />
    <a href="http://localhost:7788/third/"></a>
  <img src="http://placehold.it/400x300/a8a8a8/fff" alt="Mascot 3" />
    <a href="http://localhost:7788/third/"></a>
  <img src="http://placehold.it/400x300/989898/fff" alt="Mascot 4" />
    <a href="http://localhost:7788/third/"></a>
  <img src="http://placehold.it/400x300/888888/fff" alt="Mascot 5" />
    <a href="http://localhost:7788/third/"></a>
  <img src="http://placehold.it/400x300/787878/fff" alt="Mascot 6" />
    <a href="http://localhost:7788/third/"></a>
</div>
{% endhighlight %}

... а в файле настроек `script.js` плагина jqFancyTransitions добавить строку `links: true`:

{% highlight javascript %}
$(document).ready(function(){
  $('#slider').jqFancyTransitions({
    width: 400,
    height: 300,
    navigation: true,
    links: true
  });
});
{% endhighlight %}

Можно немного приукрасить слайдер, изменив эффект смены изображений с `zipper` на `curtain` - `effect: 'curtain'` и уменьшив задержку по времени при смене изображений `delay: 2000`:

{% highlight javascript %}
$(document).ready(function(){
  $('#slider').jqFancyTransitions({
    width: 400,
    height: 300,
    navigation: true,
    effect: 'curtain',
    delay: 2000,
    links: true
  });
});
{% endhighlight %}

Дополнительные CSS3-украшательства можно добавить по вкусу, желанию и необходимости.

## Готовый слайдер jqFancyTransitions

Примерный результат создания слайдера jqFancyTransitions может выглядеть таким образом:

![Готовый слайдер jqFancyTransitions]({{site.url}}/images/uploads/2014/06/ready_jqFancyTransitions.jpg)

Ниже показан готовый код, с помощью которого создавался подобный слайдер.

{% highlight html %}
<div class="wrapper">
  <div id="slider">
    <img src="http://placehold.it/400x300/c8c8c8/fff" alt="Mascot 1" />
      <a href="http://localhost:7788/third/"></a>
    <img src="http://placehold.it/400x300/b8b8b8/fff" alt="Mascot 2" />
      <a href="http://localhost:7788/third/"></a>
    <img src="http://placehold.it/400x300/a8a8a8/fff" alt="Mascot 3" />
      <a href="http://localhost:7788/third/"></a>
    <img src="http://placehold.it/400x300/989898/fff" alt="Mascot 4" />
      <a href="http://localhost:7788/third/"></a>
    <img src="http://placehold.it/400x300/888888/fff" alt="Mascot 5" />
      <a href="http://localhost:7788/third/"></a>
    <img src="http://placehold.it/400x300/787878/fff" alt="Mascot 6" />
      <a href="http://localhost:7788/third/"></a>
  </div>
</div>
<!-- end wrapper -->
{% endhighlight %}

{% highlight css %}
@import "compass/reset";
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
      &:first-child{
        margin-left: 0;
      }
      &:focus,&:active{
        outline: none;
      }
      &:hover{
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
{% endhighlight %}

{% highlight javascript %}
$(document).ready(function(){
  $('#slider').jqFancyTransitions({
    width: 400,
    height: 300,
    navigation: true,
    effect: 'curtain',
    delay: 2000,
    links: true
  });
});
{% endhighlight %}

На этом все - удачного кодинга!

---

 [1]: http://workshop.rs/projects/jqfancytransitions/ "jqFancyTransitions"
 [2]: http://placehold.it/ "Placehold.it"
 [3]: https://addons.mozilla.org/ru/firefox/addon/firebug/ "Firebug"
