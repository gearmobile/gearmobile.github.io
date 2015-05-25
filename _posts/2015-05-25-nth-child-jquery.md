---
title: "Метод nth-child библиотеки jQuery"
layout: post
categories: jquery
tags: [jquery,nth-child]
share: true
---

Этот метод очень похож на то, как это дело [обстоит в CSS][1]. С помощью него можно выбрать любой элемент в коллекции ему подобных, если они имеют одного общего родителя.

Приведу пример HTML-разметки, над которой буду тренироваться:

{% highlight html %}
<ul class="test">
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
</ul>
{% endhighlight %}

И начну учиться выбирать элементы из такого списка с помощью метода `.nth-child()`.

## nth-child(even) и nth-child(odd)

Такой пример javascript-кода:

{% highlight javascript %}
$(function(){
  var list = $('.test');
  list.find('li:nth-child(even)').addClass('test__item--right');
  list.find('li:nth-child(odd)').addClass('test__item--left');
});
{% endhighlight %}

... этот javascript-код читается так:

* создать переменную `list` и поместить в нее результат выборки `$('.test')`
* в переменной `list` найти все четные (even) элементы `li` - `.find('li:nth-child(even)')`
* и присвоить этим элементам `li` класс - `.addClass('test__item--right')`

{% highlight html %}
<ul class="test">
  <li class="test__item"></li>
  <li class="test__item test__item--right"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--right"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--right"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--right"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--right"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--right"></li>
</ul>
{% endhighlight %}

... затем:

* в переменной `list` найти все нечетные (odd) элементы `li` - `.find('li:nth-child(odd)')`
* и присвоить этим элементам `li` класс - `.addClass('test__item--left')`

{% highlight html %}
<ul class="test">
  <li class="test__item test__item--left"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--left"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--left"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--left"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--left"></li>
  <li class="test__item"></li>
  <li class="test__item test__item--left"></li>
  <li class="test__item"></li>
</ul>
{% endhighlight %}

Как видим, все просто и в точности также, как это [обстоит в CSS][2] с его селектором `nth-child`.

## nth-child(pattern)

Такой пример javascript-кода:

{% highlight javascript %}
$(function(){
  var list = $('.test');
  list.find('li:nth-child(2)').addClass('test__link--capitalize');
  list.find('li:nth-child(11)').addClass('test__link--uppercase');
});
{% endhighlight %}

* найдет второй элемент `li` из коллекции - `.find('li:nth-child(2)')`
* и присвоить ему класс - `.addClass('test__link--capitalize')`
* найдет 11-й элемент `li` из коллекции - `.find('li:nth-child(11)')`
* и присвоить ему класс - `.addClass('test__link--uppercase')`

{% highlight html %}
<ul class="test">
  <li class="test__item"></li>
  <li class="test__item test__link--capitalize"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item"></li>
  <li class="test__item test__link--uppercase"></li>
  <li class="test__item"></li>
</ul>
{% endhighlight %}

## Заключение

Вот и все, что можно сказать о методе `nth-child` библиотеки jQuery.

Но чуть не забыл упомянуть такой важный момент! Как уже можно было заметить, нумерация при использовании метода `nth-child` начинается не с 0, а с 1!

Впрочем, точно также обстоят дела и с селектором `nth-child` в CSS.

На этом все.

***
[1]: https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child "nth-child"
[2]: https://css-tricks.com/almanac/selectors/n/nth-child/ ":nth-child"
