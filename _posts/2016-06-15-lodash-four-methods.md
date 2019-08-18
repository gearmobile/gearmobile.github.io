---
title: 'LoDash - пять методов'
layout: post
categories: javascript
tags: [javascript]
share: true
---

Библиотека [LoDash][1] - это развитие и продолжение библиотеки [Underscore.js][3]. Если выбирать, какой библиотекой пользоваться, то выбор будет однозначно за LoDash. Достаточно сравнить колличество методов Underscore.js vs LoDash - [LoDash Documentation][2].

Еще один большой плюс LoDash - это ее модульность. Каждый ее метод доступен в виде отдельного модуля \ модулей, который \ которые можно подключить и использовать; а не "тянуть" всю библиотеку (хотя она и небольшая - 4\22 kB).

Например, подключить только методы для работы с массивами:

{% highlight javascript %}
var array = require('lodash/array');
{% endhighlight %}

Или же подключить только один метод *chunk*, чтобы уменьшить итоговую сборку:

{% highlight javascript %}
var chunk = require('lodash/chunk');
{% endhighlight %}

Или вот так - нам нужны только два модуля *random* и *foreach* для генерации случайный фоновых заливок у коллекции блоков.

Тогда можно поступить так - устанавливаем всего два модуля вместо всей библиотеки lodash:

{% highlight bash %}
$ npm i --save lodash.random
$ npm i --save lodash.foreach
{% endhighlight %}

... и используем их, ибо только они нам нужны сейчас:

{% highlight javascript %}
var random = require('lodash.random');
var forEach = require('lodash.foreach');

var items = document.querySelectorAll('.gallery\_\_item');
forEach( items, function (el) {
el.style.backgroundColor = 'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')';
});
{% endhighlight %}

В этой статье я познакомлюсь с пятью методами LoDash, которые я отложил "на потом" при знакомстве с Underscore.js. Это методы для работы с функциями - *.delay()*, *.once()*, *.after()*, *.before()*, *.debounce()*.

## lodash - .delay()

Метод *.delay()* очень прост, но тем не менее - весьма полезен на практике. Это возможность запускать функцию с временной задержкой.

Самый простой пример - через 2 секунды в консоли браузера появится сообщение *Hello World*:

{% highlight javascript %}
delay(function (text) {
console.log(text);
}, 2000, 'Hello World' );
{% endhighlight %}

Справка по этому методу в официальной документации - [Lodash - Delay][4].

## lodash - .once()

Весьма полезный метод, который позволяет запустить функцию только один раз. Приведу два примера.

Простой пример с кнопкой - *alert* выскочит только один раз при нажатии кнопки:

{% highlight javascript %}
function iAmOnce() {
alert('Hello!');
}
var callMeOnce = once(iAmOnce);
document.querySelector('#once').addEventListener('click', callMeOnce, false);
{% endhighlight %}

Второй пример интереснее. Посмотрим на разметку. Затем на javascript-код.

{% highlight html %}

<div class="block"></div>
<div id="secondo" class="block">
    <div id="count"></div>
</div>
<div class="block"></div>
<div class="block"></div>
<div class="block"></div>
<div class="block"></div>
<div class="block"></div>
<div class="block"></div>
{% endhighlight %}

Эта часть кода - украшательство, генерирование случайного цвета для каждого из блоков *class="block"* при помощи метода [.random()][5]:

{% highlight javascript %}
\$(document).ready( function () {
var blocks = document.querySelectorAll('.block');
forEach( blocks, function (el) {
el.style.backgroundColor = 'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')';
});
{% endhighlight %}

Здесь функция *callOnce()* сработает только один раз и при условии, когда блок *secondo* "поднимется" от нижней границы окна браузера на высоту 85% от общей высоты окна.

*iterrator* "отщекнется" один раз и изменит содержимое блока *id="count"* с 0 на 1:

{% highlight javascript %}
$(document).ready( function () {
    var second = $('#secondo');
var iterrator = 0;
var counter = \$('#count').text(iterrator);

    var callOnce = once( function () {
        ++iterrator;
        counter.text(iterrator);
    });

    $(window).on('scroll', function () {
        if ( $(window).scrollTop() > second.offset().top - $(window).height() * 0.85 ) {
            callOnce();
        }
    });

});
{% endhighlight %}

Весьма полезный на практике прием. Официальная справка по методу *.once()* находится здесь - [LoDash - Once Method][6].

## lodash - .before()

Метод *.before()* - счетчик выполнения функции; метод запустит функцию менее n-раз (less than n times). В приведенном ниже примере клик по элементу *#before* сработает 9 раз и запустит функцию 9 раз (и не более того):

{% highlight javascript %}
var sayHello = function () {
console.log('Hello');
};
document.querySelector('#before').addEventListener('click', before(10, sayHello), false);
{% endhighlight %}

Можно сказать и так - метод *.before()* ограничивает максимальное количество запусков функции - не более n-раз.

Официальная документация по методу *.before()* находится здесь - [LoDash - Before Method][7].

## lodash - .after()

Метод *.after()* - еще один счетчик выполнения функции. Прямая противоположность методу *.before()*.

Этот метод ограничивает количество попыток запуска функции - после n-попыток функцию можно будет запускать неограниченное количество раз:

{% highlight javascript %}
var sayAfter = function () {
console.log('After');
};
document.querySelector('#after').addEventListener('click', after(5, sayAfter), false);
{% endhighlight %}

Код выше выведет в консоль браузера текст *After* только после пятой попытки и далее сколько угодно раз. Где на практике можно применить такой подход - не приходит на ум, если честно )

Официальная документация по методу *.after()* находится здесь - [LoDash - After Method][8].

## lodash - .debounce()

Интересный и полезный на практике метод - запустить функцию *function* с временной задержкой; отсчет временной задержки идет с момента последнего запуска функции *function*.

Метод имеет большое количество аргументов - ссылка на официальную документацию - [Lodash - Debounce Method][9].

Пример ниже будет выводить окно *Call me after 2 second!* с задержкой в 2 секунды после события *resize* - то есть, когда будут изменены размеры окна браузера:

{% highlight javascript %}
var callMe = function () {
alert('Call me after 2 second!')
};
\$(window).on( 'resize', debounce( callMe, 2000 ) );
{% endhighlight %}

## Заключение

Вот я в меру своих сил и освоил несколько интересных методов библиотеки [LoDash][1]. Наиболее полезными для меня показались методы *.debounce()* и *.once()*.

Что сказать - библиотека LoDash просто замечательная и чрезвычайно полезная. К тому же она постоянно развивается - ее автор [John-David Dalton][10] не устает ее совершенствовать.

Немного пофлудил по JavaScript ... останавливаться пока не собираюсь )

---

[1]: https://lodash.com/ 'LoDash'
[2]: https://lodash.com/docs 'LoDash Documentation'
[3]: http://underscorejs.org/ 'Underscore.js'
[4]: https://lodash.com/docs#delay 'Lodash - Delay Method'
[5]: https://lodash.com/docs#random 'Lodash - Random Method'
[6]: https://lodash.com/docs#once 'LoDash - Once Method'
[7]: https://lodash.com/docs#before 'LoDash - Before Method'
[8]: https://lodash.com/docs#after 'LoDash - After Method'
[9]: https://lodash.com/docs#debounce 'Lodash - Debounce Method'
[10]: https://www.npmjs.com/~jdalton 'John-David Dalton'
