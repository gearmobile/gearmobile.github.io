---
title: "Метод first и first-child библиотеки jQuery"
layout: post
categories: jquery
tags: [jquery,first,first-child,last,last-child]
share: true
---

Рассмотрю два метода, которые похожи внешне и внутренне, как может показаться с первого взгляда. Однако, между ними есть тонкая разница.

## Метод first

Метод `first()` призван возращать первый элемент из коллекции (выборки) этих элементов. Как всегда, чтобы не быть голословным и иметь наглядный пример перед глазами, приведу ниже HTML-разметку, на которой буду тренироваться:

{% highlight html %}
<div class="wrapper">
  <ul id="primo" class="block">
    <li class="block__item"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
</div>
{% endhighlight %}

Вот такая большая разметка `div class="wrapper"` с четырьмя блоками `ul class="block"`, у каждого из которых есть элементы-потомки `li class="block__item"`.

И создам небольшой скрипт на JS/jQuery такого плана:

{% highlight javascript %}
$(function(){
  var wrapper = $('.wrapper');
  wrapper.find('li:first').addClass('block__item--firstSimple');
});
{% endhighlight %}

Работа вышеприведенного js-кода будет сводиться к следующему:

* создается переменная `wrapper`, в которую помещается результат выборки `$('.wrapper')`
* в переменной `wrapper` находим элемент `li`, который является первым в коллекции - `.find('li:first')`
* этому элементу добавляется класс - `.addClass('block__item--firstSimple')`

Код несложный и вроде бы все понятно. Но вот вопрос - а какой элемент `li` с точки зрения данного кода является первым в коллекции?

Чтобы не ломать понапрасну голову, приведу сразу ответ:

{% highlight html %}
<div class="wrapper">
  <ul id="primo" class="block">
    <li class="block__item block__item--firstSimple"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
</div>
{% endhighlight %}

Вот так - только он один и только этот элемент является первым в коллекции элементов `li`.

Это объяснимо, если слегка подумать. В переменной `wrapper` хранится коллекция элементов; и элементов `li` - в том числе.

Коллекция элементов - это не что иное, как массив. А в массиве только один элемент может быть первым. То есть, иметь индекс 0.

Именно поэтому метод `.first()` - это всего лишь синоним (alias) другого, более универсального метода `.eq()` и может быть записан таким способом - `.eq(0)` - вернуть элемент с нулевым индексом, то есть - первый элемент массива.

Антагонистом метода `.first()` является метод `last()`, который возвращает последний элемент массива. И метод `.last()` также можно записать по другому - `.eq(-1)`; это также вернет последний элемент массива.

Ок, с методом `.first()` вроде разобрались. Двигаемся дальше и рассмотрим метод `.first-child()`.

## Метод first-child()

Казалось бы, в чем разница? Трудно догадаться, поэтому сразу приведу js-код с описанием работы. В качестве подопытной HTML-разметки будет выступать все та же, приведенная в самом начале статьи.

{% highlight javascript %}
$(function(){
  var wrapper = $('.wrapper');
  wrapper.find('li:first-child').addClass('block__item--firstChild');
});
{% endhighlight %}

Что делает приведенный выше код? А вот что:

* создает переменную `wrapper` и присваивает ей значение выборки - $('.wrapper')
* в переменной `wrapper` находим первый элемент `li` - `.find('li:first-child')`
* этому элементу присваивается класс - `.addClass('block__item--firstChild')`

Все просто и вроде бы точно также, как и в случае с методом `.first()`. Вроде бы да, но возникает вопрос - а какой элемент `li` данный код считает первым в данном случае?

Чтобы не гадать, снова приведу готовый ответ:

{% highlight html %}
<div class="wrapper">
  <ul id="primo" class="block">
    <li class="block__item block__item--firstChild"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item block__item--firstChild"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item block__item--firstChild"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
  <ul class="block">
    <li class="block__item block__item--firstChild"></li>
    <li class="block__item"></li>
    <li class="block__item"></li>
  </ul>
</div>
{% endhighlight %}

Вот она - разница в подходе отбора первого элемента. Другими словами, метод `.first-child()` находит все элементы, которые являются первыми потомками у своих непосредственных родителей. А в данном случае таких потомков насчиталось аж 4 штуки.

Конечно, можно провести аналогию и рассмотреть метод `.last-child()`. Но мне кажется, смысла в этом особого нет - все и так понятно. Выборка будет производиться с точностью до наоборот и будут отбираться последние потомки своих неспосредственных родителей.

На этом думаю закончить сравнительный обзор двух методов - `.first()` и `.first-child()`.

***
