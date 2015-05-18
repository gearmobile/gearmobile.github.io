# Метод eq и index библиотеки jQuery

Достаточно интересные методы - `.eq()` и `.index()`, особенно в сочетании друг с другом. Поэтому и решил объединить рассмотрение этих методов. Каждый по отдельности - методы просты и мало показательны.

Но для начала вкратце (по другому и не получиться) опищу каждый из методов, по возможности своими словами.

## Метод index

Работа метода `.index()` проста - он возвращает индекс (порядковый номер) указанного элемента среди группы ему подобных.

Синтаксис метода `.index()` также простой:

{% highlight javascript %}
index([element])
{% endhighlight %}

или

{% highlight javascript %}
.index(selector)
{% endhighlight %}

И пример для иллюстрации:

{% highlight html %}
<ul class="test">
  <li class="primo">
    <a href="#" class="test__link">test item link</a>
  </li>
  <li class="secondo">
    <a href="#" class="test__link">test item link</a>
  </li>
  <li class="tetro">
    <a href="#" class="test__link">test item link</a>
  </li>
  <li class="quattro">
    <a href="#" class="test__link">test item link</a>
  </li>
  <li class="cinque">
    <a href="#" class="test__link">test item link</a>
  </li>
  <li class="sei">
    <a href="#" class="test__link">test item link</a>
  </li>
  <li class="sedici">
    <a href="#" class="test__link">test item link</a>
  </li>
  <li class="ten">
    <a href="#" class="test__link">test item link</a>
  </li>
</ul>
{% endhighlight %}

Сделать выборку всех элементов `li` и вернуть индекс элемента `li` с классом `.cinque`:

{% highlight javascript %}
var listIndex = $('.cinque');
console.log('Index of ' + $('li').index(listIndex));
{% endhighlight %}

Найти элемент с классом `.sei` среди соседних элементов и вернуть его индекс:

{% highlight javascript %}
console.log('Index of ' + $('.sei').index());
{% endhighlight %}

Как видим, способы получения индекса элемента разные, а результат один.

## Метод eq

Метод `.eq()` прямопротивоположен методу `.index()`. Этот метод возвращает элемент (как объект) по его индексу (порядковому номеру).

Если взять предыдущую HTML-разметку, то такой javascript-код:

{% highlight javascript %}
$('li').eq(1).html("Secondo");
{% endhighlight %}

... изменит содержимое второго по счету элемента `li` на "Secondo". Почему второго? Как можно догадаться, результатом выборки `$('li')` является массив элементов; а в массиве индексирование элементов начинается с нуля (0).

## Методы eq и index

Рассмотренные выше примеры использования методов `.eq()` и `.index()` просты и понятны. И неинтересны.

Гораздо более интеерсным примером является случай объединения обоих методов в jQuery-цепочке.

Приведу такой гипотетический пример:

{% highlight html %}
<ul class="test">
  <li class="test__item primo"><a href="#" class="test__link">test item link</a></li>
  <li class="test__item secondo"><a href="#" class="test__link">test item link</a></li>
  <li class="test__item tetro"><a href="#" class="test__link">test item link</a></li>
  <li class="test__item quattro"><a href="#" class="test__link">test item link</a></li>
  <li class="test__item cinque"><a href="#" class="test__link">test item link</a></li>
  <li class="test__item sei"><a href="#" class="test__link">test item link</a></li>
  <li class="test__item sedici"><a href="#" class="test__link">test item link</a></li>
  <li class="test__item"><a href="#" class="test__link">test item link</a></li>
</ul>
{% endhighlight %}

{% highlight javascript %}
$('.test__item').click(function(){
  $('li').eq($(this).index()).html($(this).index()).siblings().html("test item link");
});
{% endhighlight %}

Javascript-код, написанный выше, читается таким образом:

* сделать выборку всех элементов с классом `.test__item`
* при клике мыши на любом из этих элементов выполнить функцию
* сделать выборку всех элементов `li`
* вернуть индекс активного элемента из выборки - `$(this).index()`
* вернуть активный элемент по его индексу - `.eq($(this).index())`
* для возвращенного элемента `.eq($(this).index())` изменить его содержимое на значение его индекса - `html($(this).index())`
* всем соседним (sibling) элементам установить значение в - `.siblings().html("test item link")`

Пример рабочий, поэтому его можно свободно попробовать.

В принципе, на этом все.

***
