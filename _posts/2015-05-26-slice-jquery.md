---
title: "Метод slice библиотеки jQuery"
layout: post
categories: jquery
tags: [jquery,slice]
share: true
---

Достаточно интересный (для меня) метод выборки элеемнтов из коллекции - метод `.slice()`. Хотя чего-то эдакого в этом методе не совсем.

Просто этот метод позволяет установить диапазон (область), по которому (внутри которой) будут выбираться элементы.

Синтаксис метода `.slice()` таков:

{% highlight javascript %}
.slice(start,[end])
{% endhighlight %}

Возвращает элементы с индексами от `start` до `end`, если последний задан или до конца, если параметр `end` опущен.

Элементы с индексом `start` включаются в результат, а `end` - нет (т.е. `.slice(3,5)` вернет элементы, идущие под индексом 3 и 4, элемент с индексом 5 включен не будет).

Кроме этого, параметры могут быть заданы в форме отрицательных чисел, в таком случае, отсчет элементов идет с конца набора: `-1` – последний элемент, `-2` – предпоследний элемент и т. д.

## Примеры использования:

`$("div").slice(3)` - вернет все div-элементы, начиная с четвертого (с индексами 3, 4, ...)
`$("div").slice(3, 5)` - вернет div-элементы с индексами 3 и 4
`$("div").slice(-4, -2)` - вернет div-элементы, идущие четвертым и третьим с конца
`$("div").slice(-2)` - вернет предпоследний и последний div-элементы на странице

Приведу пример HTML-разметки:

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

Такой javascript-код:

{% highlight javascript %}
$(function(){
  var list = $('.test');
  list.find('li').slice(2,10).addClass('test__link--sliced');
});
{% endhighlight %}

... выполнит следующее:

* создаст переменную `list` и поместит в нее результат выборки - `$('.test')`
* найдет в переменной `list` все элементы `li` - `.find('li')`
* в найденной коллекции определит диапазон элементов `li` с индексами с 2-го по 10-й - `.slice(2,10)`
* добавит к элементам `li` этого диапазона класс - `.addClass('test__link--sliced')`
* но не добавит класс `.test__link--sliced` к элементу `li` с индексом 10!

Результатом выполнения показанного выше js-кода будет такая HTML-разметка:

{% highlight html %}
<ul class="test">
  <li class="test__item"><a href="#" class="test__link">test link item 1</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 2</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 3</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 4</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 5</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 6</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 7</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 8</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 9</a></li>
  <li class="test__item test__link--sliced"><a href="#" class="test__link">test link item 10</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 11</a></li>
  <li class="test__item"><a href="#" class="test__link">test link item 12</a></li>
</ul>
{% endhighlight %}

Обратите внимание, что нумерация элементов начинается с `0` - это индекс элемента! Элемент с последним индексом не включен в выборку!

Еще один пример, более краткий и наглядный.

Начальный HTML-код:

{% highlight html %}
<ul class="bad">
  <li class="bad__item"></li>
  <li class="bad__item"></li>
  <li class="bad__item"></li>
  <li class="bad__item"></li>
  <li class="bad__item"></li>
  <li class="bad__item"></li>
  <li class="bad__item"></li>
</ul>
{% endhighlight %}

JavaScript-код:

{% highlight javascript %}
$(function(){
  var bad = $('.bad');
  bad.find('li').slice(2,4).addClass('bad__item--sliced');
});
{% endhighlight %}

Результат:

{% highlight html %}
<ul class="bad">
  <li class="bad__item"></li>
  <li class="bad__item"></li>
  <li class="bad__item bad__item--sliced"></li>
  <li class="bad__item bad__item--sliced"></li>
  <li class="bad__item"></li>
  <li class="bad__item"></li>
  <li class="bad__item"></li>
</ul>
{% endhighlight %}

На этом все. Материал частично основан на ресурсе [jquery.page2page][1] и не претендует на оригинальность.

***
[1]: http://jquery.page2page.ru/ "jQuery Page2Page"
