---
title: "JavaScript - Dice Game"
layout: post
categories: javascript
tags: [javascript, game, dice]
share: true
---

Создание игры Dice Game (игра в кости) на JavaScript. Вот нашлось время и силы познакомиться с игрой такого типа. Сразу оговорюсь, что материал и пример не мой, а взят из зарубежного ресурса для изучения.

В примере рассмотрен основной принцип создания игры Dice. Можно сказать - чисто схематично. Однако этого достаточно, чтобы остальное дополнить по необходимости.

Код оказался на удивление прост. Я не сомневаюсь, что в Интернете есть примеры более сложного и совершенного JavaScript-кода для игр подобного типа. Но цель статьи - познакомиться с основным принципом создания игры, не более.

## HTML разметка и стили

Разметка очень простая и состоит из четырех элементов:

{% highlight html %}
<div class="wrapper">
    <div class="column">
        <div id="dice-side-1" class="dice">0</div>
        <div id="dice-side-2" class="dice">0</div>
    </div>
    <div class="column">
        <button type="button" class="dice-roll">roll dice</button>
        <h2 id="status"></h2>
    </div>
</div>
{% endhighlight %}

Элементы `id="dice-side-1"` и `id="dice-side-2"` - это иммитация двух игральных костей; как если бы эти кости были обращены лицевой стороной к зрителю.

Кнопка `class="dice-roll"` служит для управления; с помощью нее мы будем "бросать" игральные кости.

Заголовок `id="status"` носит информативный характер - в нем будет выводиться текущая информация.

CSS-стили в комментариях не нуждаются, ибо они небольшого размера и "прозрачные":

{% highlight css %}
body {
    position: relative;
}

.wrapper {
    width: 400px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
}

.column {
    display: flex;
    align-items: center;
}

#status {
    position: absolute;
    top: 1rem;
    right: 1rem;
    min-width: 400px;
    margin: 0;
}

.dice {
    width: 32px;
    float: left;
    background-color: lightcoral;
    border: 1px solid black;
    padding: 10px;
    font-size: 24px;
    text-align: center;
    margin: 5px;
    border-radius: 5px;
}

.dice-roll {
    cursor: pointer;
    text-transform: capitalize;
}
{% endhighlight %}

## JavaScript - оживляем игральные кости

Далее приступим к более интересной части задачи - созданию js-кода для "оживления" наших игральных костей.

Для этого "выберем" из HTML кнопку и "повесим" на нее функцию rollDice для обработки клика по кнопке:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

    var buttonRollDice = document.querySelector('.dice-roll');
    buttonRollDice.addEventListener('click', rollDice, false);

}, false);
{% endhighlight %}

Затем начнем описывать функцию rollDice. Создадим три переменные, в которые поместим обе игральные кости и информативный заголовок:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

    function rollDice () {

        var diceSide1 = document.getElementById('dice-side-1');
        var diceSide2 = document.getElementById('dice-side-2');
        var status = document.getElementById('status');

    }

}, false);
{% endhighlight %}

Сгенерируем два случайных числа из диапазона от 1 до 6. Игральная кость имеет шесть сторон - поэтому такой диапазон. Эти числа будут иммитацией одной из шести сторон каждой игральной кости.

Другими словами. На всех сторонах игрального кубика "выбито" точками число - от 1 до 6. Поэтому можно сказать иначе - диапазон от 1 до 6 - это диапазон возможных значений, которые выпадают на каждой из игральных костей:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

    function rollDice () {

        var diceSide1 = document.getElementById('dice-side-1');
        var diceSide2 = document.getElementById('dice-side-2');
        var status = document.getElementById('status');

        var side1 = Math.floor( Math.random() * 6 ) + 1;
        var side2 = Math.floor( Math.random() * 6 ) + 1;
        var diceTotal = side1 + side2;

    }

}, false);
{% endhighlight %}

Переменная `diceTotal` служит для информативных целей - будем показывать сообщение о том, сколько в сумме выпало очков на игральных костях.

Осталось поместить случайно сгенерированную пару чисел в HTML-код. Помимо этого вывести информационное сообщение, сколько очков в сумме выпало. И предупредить, если на обеих костях выпавшее число одинаковое - тогда предоставить игроку еще один ход:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

    function rollDice () {

        var diceSide1 = document.getElementById('dice-side-1');
        var diceSide2 = document.getElementById('dice-side-2');
        var status = document.getElementById('status');

        var side1 = Math.floor( Math.random() * 6 ) + 1;
        var side2 = Math.floor( Math.random() * 6 ) + 1;
        var diceTotal = side1 + side2;

        diceSide1.innerHTML = side1;
        diceSide2.innerHTML = side2;

        status.innerHTML = 'You rolled ' + diceTotal + '.';

        if ( side1 === side2 ) {
            status.innerHTML += ' Doubles! You get a free turn!';
        }
    }

}, false);
{% endhighlight %}

Наш JavaScript-код готов и выглядит таким несложным способом:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

    function rollDice () {

        var diceSide1 = document.getElementById('dice-side-1');
        var diceSide2 = document.getElementById('dice-side-2');
        var status = document.getElementById('status');

        var side1 = Math.floor( Math.random() * 6 ) + 1;
        var side2 = Math.floor( Math.random() * 6 ) + 1;
        var diceTotal = side1 + side2;

        diceSide1.innerHTML = side1;
        diceSide2.innerHTML = side2;

        status.innerHTML = 'You rolled ' + diceTotal + '.';

        if ( side1 === side2 ) {
            status.innerHTML += ' Doubles! You get a free turn!';
        }
    }

    var buttonRollDice = document.querySelector('.dice-roll');
    buttonRollDice.addEventListener('click', rollDice, false);

}, false);
{% endhighlight %}

Готовый пример Dice Game можно потестить по этой ссылке - [JavaScript Dice Game](http://codepen.io/gearmobile/pen/mEJwYw "JavaScript Dice Game").

## Заключение

В заключение, как мне кажется, стоит сказать пару слов по поводу рассмотренного примера. Он является достаточно схематичным. Однако никто не мешает дополнить код возможностью смены изображений, иммитирующих грани костей.

Плюс - добавить анимацию. И получится весьма неплохой результат, как мне представляется.

***

На этом все.
