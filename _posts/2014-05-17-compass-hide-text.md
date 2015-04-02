---
title: "Замена текста изображением в Compass"
layout: post
categories:
tags: [compass, text-replacement]
share: true
---

> При верстке макета довольно часто возникает задача создания кликабельного логотипа страницы.

Но логотип страницы, как правило, создается с использованием на все 100% фантазии дизайнера - тут и необычный декоративный шрифт, и всякие добавленные в него изображения. Поэтому на практике обычно такой логотип вырезается из psd-макета целиком, в виде картинки.

В HTML-разметке в заголовке страницы помещается текст-логотип сайта в теге первого уровня `h1` - все по правилам SEO. А в таблицах стилей производится подмена текста на вырезанное из макета изображение.

В результате удается выйти из положения, когда и овцы целы и волки сыты. В этой статье будут рассмотрены несколько способов, с помощью которых можно решить данную задачу. Причем, решить наиболее простым и быстрым способом, с помощью миксинов благодаря волшебной библиотеке Compass.

Первоначально произведем подключение неоходимого модуля в библиотеке Compass, добавив строку импортирования в проект:

{% highlight css %}
@import "compass/typography/text/replacement";
{% endhighlight %}

... а затем приступим к изучению миксинов.

## Миксин hide-text

Первым миксином, который решает задачу замены текста изображением, является `hide-text`.

Синтаксис этого миксина таков:

{% highlight css %}
@include hide-text([$direction])
{% endhighlight %}

... где необязательный аргумент `$direction` определяет направление скрытия текста.

Пример использования данного миксина:

{% highlight html %}
<h1 class="hidetext">
  mixin hide-text
</h1>
{% endhighlight %}

{% highlight css %}
.hidetext{
  margin: 10px auto;
  width: 640px;
  height: 426px;
  background: url(../img/cat.jpg) 0 0 no-repeat;
}
{% endhighlight %}

![Текст с фоновым изображением]({{site.url}}/images/uploads/2014/05/text_replacement_01.jpg)

Подключим к вышеприведенному коду миксин `hide-text` и посмотрим на результат:

{% highlight css %}
.hidetext{
...
  @include hide-text;
}
{% endhighlight %}

![Результат замещения текста с помощью миксина hide-text]({{site.url}}/images/uploads/2014/05/text_replacement_hide-text.jpg)

Результирующий CSS-код будет выглядеть таким образом. Добавляются смещение текста с помощью свойства `text-indent` с отрицательным значением; предотвращается случайное "схлопывание" блока через свойство `overflow: hidden`, если в нем вдруг окажутся плавающие элементы; задается расположение текста с левого края блока через свойство `text-align: left`, чтобы гарантировать его смещение за левый край блока через свойство `text-indent`:

{% highlight css %}
.hidetext{
  ...
  text-indent: -119988px;
  overflow: hidden;
  text-align: left;
}
{% endhighlight %}

## Миксин squish-text

В библиотеке Compass также имеется миксин `squish-text` для замещения текста изображением с помощью **эффекта скрытия** данного текста. Другими словами, текст остается на своем месте, просто с помощью определенных CSS-свойств он делается визуально невидимым. Это может быть удобно для браузеров-читалок, которые проговаривают текст вслух для слабовидящих людей.

Синтаксис миксина `squish-text` таков:

{% highlight css %}
@include squish-text;
{% endhighlight %}

Пример использования миксина `squish-text`:

{% highlight html %}
<h1 class="squishtext">
  Mixin squish-text
</h1>
{% endhighlight %}

{% highlight css %}
...
.squishtext{
  color: white;
  text-align: center;
  font-size: 3em;
  font-weight: bold;
  margin: 10px auto;
  width: 640px;
  height: 480px;
  background: url(../img/girl.jpg) 0 0 no-repeat;
}
{% endhighlight %}

![Текст с фоновым изображением]({{site.url}}/images/uploads/2014/05/text_replacement_02.png)

Подключим миксин `squish-text` и посмотрим на результат его работы:

{% highlight css %}
.squishtext{
  ...
  @include squish-text;
}
{% endhighlight %}

![Результат замещения текста с помощью миксина squish-text]({{site.url}}/images/uploads/2014/05/text_replacement_squish-text.png)

Результат компилирования представленного выше SCSS-кода в CSS-код показан ниже. Довольно интересный способ скрытия текста, который стоит рассмотреть более подробно. С помощью CSS-свойства `font` сбрасывается на ноль размер шрифта (*кегль*) и межстрочное расстояние (интерлиньяж) для текста. Цвет текста через CSS-свойство `color` устанавливается прозрачным. В добавок гарантированно убирается тень у текста, если она у него есть (вдруг сработает наследование).

{% highlight css %}
.squishtext {
  ...
  font: 0/0 serif;
  text-shadow: none;
  color: transparent;
}
{% endhighlight %}

Несмотря на то, что визуально результат работы миксина `squish-text` аналогичен работе миксина `hide-text`, принцип последнего более эффективен для большинства современных браузеров в вопросе замещения inline-текста.

В показанном ниже примере можно улучшить разметку, "обернув" отдельные участки текста в любой из inline-элементов (`span`, `b` или `i`) и добавив к нему ноебходимый класс:

{% highlight html %}
<p class="squish">Lorem ipsum dolor sit amet,<span class="squish-text"> consectetur adipisicing elit,</span> sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor <span class="squish-text">in reprehenderit in voluptate velit esse</span> cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat <span class="squish-text">cupidatat non proident</span>, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
{% endhighlight %}

{% highlight css %}
.squish{
  margin: 0 auto;
  @include margin-leader;
  max-width: 960px;
  font-family: 'PT Sans', sans-serif;
  .squish-text{
    color: hsla(240,100%,50%,.6);
    font-style: italic;
  }
}
{% endhighlight %}

![Текст с отдельными участками, подлежащими скрытию]({{site.url}}/images/uploads/2014/05/text_replacement_03.png)

{% highlight css %}
.squish{
  ...
  .squish-text{
    ...
    @include squish-text;
  }
}
{% endhighlight %}

В то время, как экранные программы-читалки и другие подобные инструменты могут свободно прочитать "спрятанный" текст, в окне обычного браузера он ни как не отображен:

![Скрытие текста с помощью миксина squish-text]({{site.url}}/images/uploads/2014/05/text_replacement_squish-text_text.png)

## Замещение текста изображением с фиксированными размерами

Если не принимать во внимание технологию спрайтов для фонового изображения, в Compass существует другой миксин, который также позволяет удобно замещать текст изображением. Это полезно, например, когда нужно поместить изображение логотипа в тег заголовка.

Преимущество данного миксина заключается в автоматизированном способе установки размеров для элемента в соответствии с размерами используемого изображения. Для этой цели в библиотеке Compass имеется миксин с говорящим названием `replace-text-with-dimensions`:

{% highlight css %}
@include replace-text-with-dimensions();
{% endhighlight %}

Проиллюстрируем применение миксина `replace-text-with-dimensions`:

{% highlight html %}
<h1 class="replace_dimensions">
  replace-text-with-dimensions
</h1>
{% endhighlight %}

![Текст с непримененным миксином replace-text-with-dimensions]({{site.url}}/images/uploads/2014/05/text_replacement_04.png)

{% highlight css %}
.replace_dimensions{
  @include replace-text-with-dimensions('alsatian.jpg');
}
{% endhighlight %}

Не забудьте активировать строку `relative_assets = true` в конфигурационном файле `config.rb`, чтобы сработали относительные пути для изображений!

![Текст с примененным миксином replace-text-with-dimensions]({{site.url}}/images/uploads/2014/05/text_replacement_replace-text-with-dimensions.png)

Мне кажется, было бы очень любопытно взглянуть на результирующий код компиляции в CSS. Видим, что на изображение указывает корректная ссылка; а также, что у изображения установлены правильные ширина (`width`) и высота (`height`). Все это благодаря Compass!

{% highlight css %}
.replace_dimensions {
  text-indent: -119988px;
  overflow: hidden;
  text-align: left;
  background-image: url('../img/alsatian.jpg?1400248446');
  background-repeat: no-repeat;
  background-position: 50% 50%;
  width: 640px;
  height: 470px;
}
{% endhighlight %}

## Замена текста изображением в HTML5 Boilerplate

За годы существования веб-разработки было создано немало оригинальных способов замещения текста изображением. На сегодняшний день наиболее лучшим способом является техника, представленная в хорошо известном проекте [HTML5 Boilerplate][1].

Ниже показан пример исходного CSS-кода, взятого из "HTML5 Boilerplate", в котором показаны в виде классов различные способы замещения текста изображением. В каждом случае кратко описываются преимущества каждого из способов:

{% highlight css %}
.ir {
    background-color: transparent;
    border: 0;
    overflow: hidden;
    /* IE 6/7 fallback */
    *text-indent: -9999px;
}

.ir:before {
    content: "";
    display: block;
    width: 0;
    height: 150%;
}

// Скрыть текст от экранных читалок и браузеров

.hidden {
    display: none !important;
    visibility: hidden;
}

// Скрыть текст только визуально, но оставить доступным для экранных читалок

.visuallyhidden {
    border: 0;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
}

// Расширение класса .visuallyhidden благодаря возможности для элементов получать фокус с клавиатуры

.visuallyhidden.focusable:active,
.visuallyhidden.focusable:focus {
    clip: auto;
    height: auto;
    margin: 0;
    overflow: visible;
    position: static;
    width: auto;
}

// Скрыть текст визуально и от экранных читалок, но оставить нетронутой HTML-разметку

.invisible {
    visibility: hidden;
}
{% endhighlight %}

На этом все. Данная статья является вольным переводом отдельной главы из книги **Ben Frain "Sass and Compass for Designers**".

---

[1]: http://html5boilerplate.com "HTML5 Boilerplate"
