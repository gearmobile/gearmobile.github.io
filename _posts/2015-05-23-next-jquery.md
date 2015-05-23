---
title: "Методы next и prev библиотеки jQuery"
layout: post
categories: jquery
tags: [jquery, next, prev, nextAll, prevAll]
share: true
---

Рассмотрю методы для нахождения **следующих** и **предыдущих** элементов из выборки. Предполагается, что имеется группа элементов, у которых один родитель.

Чтобы не ходить вокруг да около, приведу пример HTML-разметки:

{% highlight html %}
<ul class="test">
  <li class="test__item"><a href="#" class="test__link">test link item 1</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 2</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 3</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 4</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 5</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 6</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 7</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 8</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 9</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 10</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 11</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 12</a></li>
</ul>
{% endhighlight %}

Видно, что у элемента-родителя `ul class="test"` имеется двенадцать элементов-потомков `li class="test__item"`.

Так вот, в библиотеке jQuery имеются несколько методов, с помощью которых можно "погулять" по этому DOM-дереву. Расссмотрю каждый из них в отдельности.

Но стоит сразу сказать - как всегда, эти методы очень краткие и предельно понятные. Вся "прелесть" начинается, когда методы объединяют в jQuery-цепочку.

## Метод next()

С помощью этого метода возвращается элемент, находящий **следующим** по отношению к текущему элементу.

Приведу такой JS-код:

{% highlight javascript %}
$(function(){
  var list = $('.test');
  list.find('li').eq(6).next().addClass('test__link--nexted');
});
{% endhighlight %}

... который выполняет следующее:

* создать переменную `list` и поместить в нее результат выборки `$('.test')`
* в переменной `list` найти все элементы `li`
* вернуть элемент `li` с индексом 6 - `.eq(6)`
* найти следующий за ним элемент `li`
* присвоить ему класс `.test__link--nexted`

В результате выполнения этого кода класс `.test__link--nexted` будет присвоен элементу `li` с индексом 7 (или восьмому - по счету):

{% highlight html %}
<ul class="test">
  <li class="test__item"><a href="#" class="test__link">test link item 1</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 2</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 3</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 4</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 5</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 6</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 7</a></li>
  <li class="test__item test__link--nexted"><a href="#" class="test__link">test link item 8</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 9</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 10</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 11</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 12</a></li>
</ul>
{% endhighlight %}

## Метод prev()

Этот метод абсолютно аналогичен методу `next()` за тем исключением, что его действие направлено в противоположную сторону. Метод `prev()` возвращает элемент, который **предшествует** текущему элементу.

То есть, такой JS-код:

{% highlight javascript %}
$(function(){
  var list = $('.test');
  list.find('li').eq(6).prev().addClass('test__link--preved');
});
{% endhighlight %}

* создаст переменную `list` и поместит в нее результат выборки `$('.test')`
* в переменной `list` найдет все элементы `li`
* вернет элемент `li` с индексом 6 - `.eq(6)`
* найдет предшествующий ему элемент `li`
* присвоит ему класс `.test__link--preved`

Результатом выполнения этого кода класс `.test__link--preved` будет присвоен элементу `li` с индексом 5 (или шестому - по счету):

{% highlight html %}
<ul class="test">
  <li class="test__item"><a href="#" class="test__link">test link item 1</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 2</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 3</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 4</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 5</a></li>
  <li class="test__item test__link--preved"><a href="#" class="test__link">test link item 6</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 7</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 8</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 9</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 10</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 11</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 12</a></li>
</ul>
{% endhighlight %}

### Краткое заключение

Обобщением вышесказанного является такое предложение. Методы `next()` и `prev()` возвращают один элемент, который является **следующим** или **предшествует** текущему элементу. Все элементы имеют **одного общего родителя** и поиск осуществляется только в этих рамках (другими словами - это sibling-элементы).

## Методы nextAll() и prevAll()

Производными от рассмотренных мною выше методов `next()` и `prev()` являются методы `nextAll()` и `prevAll()`. Фактически, это те же самые методы `next()` и `prev()`, но в этих методах возвращается не один элемент, а **все оставшиеся** элементы, которые являются sibling по отношению к текущему элементу.

То есть, такой JS-код:

{% highlight javascript %}
$(function(){
  var list = $('.test');
  list.find('li').eq(3).nextAll().addClass('block__item--squared');
});
{% endhighlight %}

* создаст переменную `list` и поместит в нее результат выборки `$('.test')`
* в переменной `list` найдет все элементы `li`
* вернет элемент `li` с индексом 3 - `.eq(3)`
* найдет все следующие за ним элементы `li` - `.nextAll()`
* присвоит всем найденным элементам `li` класс `.block__item--squared`

Результатом будет такой HTML-код:

{% highlight html %}
<ul class="test">
  <li class="test__item"><a href="#" class="test__link">test link item 1</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 2</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 3</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 4</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 5</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 6</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 7</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 8</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 9</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 10</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 11</a></li>
  <li class="test__item block__item--squared"><a href="#" class="test__link">test link item 12</a></li>
</ul>
{% endhighlight %}

Метод `prevAll()` работает аналогично, но "в другую сторону". Этот метод возвращает **все элементы**, которые **предшествуют** текущему элементу.

То есть, такой JS-код:

{% highlight javascript %}
$(function(){
  var list = $('.test');
  list.find('li').eq(3).prevAll().addClass('block__item--circled');
});
{% endhighlight %}

* создаст переменную `list` и поместит в нее результат выборки `$('.test')`
* в переменной `list` найдет все элементы `li`
* вернет элемент `li` с индексом 3 - `.eq(3)`
* найдет все элементы `li`, которые предшествуют ему - `.prevAll()`
* присвоит всем найденным элементам `li` класс `.block__item--circled`

Результатом работы этого js-скрипта будет такой HTML-код:

{% highlight html %}
<ul class="test">
  <li class="test__item block__item--circled"><a href="#" class="test__link">test link item 1</a></li>
  <li class="test__item block__item--circled"><a href="#" class="test__link">test link item 2</a></li>
  <li class="test__item block__item--circled"><a href="#" class="test__link">test link item 3</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 4</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 5</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 6</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 7</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 8</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 9</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 10</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 11</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 12</a></li>
</ul>
{% endhighlight %}

## Общее заключение

Вывод по методам `nextAll()` и `prevAll()`. Эти методы работают с sibling-элементами, то есть - имеющими одного родителя. Эти методы возвращают все найденные элементы, которые предшествуют или расположены после текущего элемента.

Методы `nextAll()` и `prevAll()` очень похожи также на рассмотренный мною в предыдущей статье метод `siblings`. Вот только действие метода `siblings` более "тупое" (если позволительно так сказать) - этот метод "фигачит" свое действие сразу в обе стороны от текущего элемента, по принципу - "от забора и до обеда".

Методы `nextAll()` и `prevAll()` более "интеллектуальные" - они "фигачат" свое действие только в одну сторону - указанную.

Ну, а методы `next()` и `prev()` самые "умные" - "только один элемент, который ближайший и слева"; "только один элемент, который ближайший и справа".

На этом все.

***
