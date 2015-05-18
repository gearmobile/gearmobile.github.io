## Метод siblings библиотеки jQuery

Небольшое отступление - в одних постах я говорю о функциях jQuery, в других - о методах jQuery. Где же правильно? В принципе, и то и то правильно. И функция jQuery, и метод jQuery. Но последний вариант более правильный, поэтому в дальнейшем буду "обзывать" подобные вещи методами.

Метод `.siblings()` предназначен для выборки соседних элементов. С помощью этого метода выбираются все элементы, находящиеся на одном уровне DOM с элементом, служащим в качестве критерия отбора.

Метод имеет один вариант использования (синтаксис):

{% highlight html %}
.parent([selector])
{% endhighlight %}

Все очень похоже на то, как эти дела [обстоят в CSS][1], но приведу простой пример для иллюстрации:

{% highlight html %}
<nav class="test">
  <a href="javascript:void(0);" class="test__link">test link item</a>
  <a href="javascript:void(0);" class="test__link">test link item</a>
  <a href="javascript:void(0);" class="test__link proba">test link item</a>
  <a href="javascript:void(0);" class="test__link">test link item</a>
  <a href="javascript:void(0);" class="test__link">test link item</a>
</nav>
{% endhighlight %}

{% highlight javascript %}
$('.proba').siblings().addClass('selected');
{% endhighlight %}

... **читается это так** - добавить класс `.selected` для всех элементов, соседних (sibling) с элементом, имеющим класс `.proba`. То есть, класс `.selected` будет добавлен всем элементам `a`, так как они находятся на одном уровне DOM с элементом `.proba` и являются соседними по отношению к нему.

По умолчанию можно не передавать методу `.siblings()` аргумент в виде селектора - `.siblings('a')`, так как подразумеваются элементы, которые являются соседними в текущей HTML-разметке. Но можно передавать методу в качестве аргумента имя класса  - `.siblings('.test__link')`; или элемент с именем класса (идентификатора) - `.siblings('a.test__link')`.

Краткие примеры использования метода `.siblings()`, взятые с ресурса [jQuery Page2Page][2]:

* `$("#block").siblings()` - найдет элементы, которые имеют общего родителя с элементом, обладающим идентификатором `#block`
* `$(".lBlock").siblings()` - найдет элементы, которые имеют общих родителей с элементами класса `.lBlock`
* `$(".lBlock").siblings(".cont")` - найдет элементы класса `.cont`, которые имеют общих родителей с элементами класса `.lBlock`

Важный момент - в этом случае класс `.selected` не будет добавлен к элементу `.proba`. Другими словами, в методе `.siblings()` к элементу, служащему в качестве критерия, не применяются действия этого метода.

Чтобы было еще понятнее, о чем идет речь, представлю ниже результат работы описанного выше javascript-кода:

{% highlight html %}
<nav class="test">
  <a href="javascript:void(0);" class="test__link selected">test link item</a>
  <a href="javascript:void(0);" class="test__link selected">test link item</a>
  <a href="javascript:void(0);" class="test__link proba">test link item</a>
  <a href="javascript:void(0);" class="test__link selected">test link item</a>
  <a href="javascript:void(0);" class="test__link selected">test link item</a>
</nav>
{% endhighlight %}

Метод `.siblings()` прост и понятен. Единственным "подводным камнем" при работе с ним является такой момент - нужно быть внимательным с **уровнями вложения элементов**. Другими словами, в дереве DOM элементы не расположены на одном уровне (не являются sibling), однако разработчик упрямо пытается применить к этим элементам метод `.sibling()`. И потом сильно недоумевает, почему ничего не работает, хотя код то правильный!

Приведу простой пример такой ошибки, с которой один раз сам столкнулся. Здесь пример кристально ясный и понятный, однако на деле все было не так прозрачно (в совокупности с другим кодом):

{% highlight html %}
<ul class="test">
  <li class="test__item">
    <a href="javascript:void(0);" class="test__link">test item link</a>
  </li>
  <li class="test__item">
    <a href="javascript:void(0);" class="test__link">test item link</a>
  </li>
  <li class="test__item">
    <a href="javascript:void(0);" class="test__link proba">test item link</a>
  </li>
  <li class="test__item">
    <a href="javascript:void(0);" class="test__link">test item link</a>
  </li>
  <li class="test__item">
    <a href="javascript:void(0);" class="test__link">test item link</a>
  </li>
</ul>
{% endhighlight %}

{% highlight javascript %}
$('.proba').siblings().addClass('selected');
{% endhighlight %}

Представленный выше javascript-код **работать не будет**, так как элементы `a` (а код был сделан в расчете на эти элементы) соседними (siblings) не являются. Это хорошо заметно, если внимательно рассмотреть HTML-код примера.

Вот, в принципе, и все, что можно сказать о методе `.siblings()`.

На этом все.

***

[1]: https://css-tricks.com/child-and-sibling-selectors/ "Child and Sibling Selectors"
[2]: http://jquery.page2page.ru/ "Siblings jQuery"
