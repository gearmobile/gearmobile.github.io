---
title: "JavaScript - создаем калькулятор"
layout: post
categories: javascript
tags: [javascript]
share: true
---

Обзор посвящен созданию JavaScript-калькулятора. Домашнее задание для каждого начинающего JavaScript-ниндзя! ) В коде используется не чистый JavaScript, а JavaScript + jQuery.

Пример и материал не является оригинальным, основан на зарубежном источнике. Указывать источник не буду, потому что это не имеет смысла - таких кратких видеоуроков просто огромное количество - выбирай любой, какой понравится. )

## HTML разметка

HTML-разметка для будущего калькулятора основана на HTML-элементах `form`, `input`, `button`. Ничего сверхестественного в ней нет.

Единственный момент - вопрос компоновки кнопок, куда правильно "засунуть" кнопки с арифметическими операциями:

{% highlight html %}
<!-- CALCULATOR -->
<div class="calculator">
    <!-- CALCULATOR FORM -->
    <form class="calculator__form">
        <!-- CALCULATOR ROW -->
        <div class="calculator__row">
            <input class="calculator__display" id="display" type="text" disabled />
        </div>
        <!-- CALCULATOR ROW -->
        <div class="calculator__row">
            <button type="button" value="c" class="calculator__key calculator__clear"></button>
            <button type="button" value="<--" class="calculator__key calculator__backspace"></button>
            <button type="button" value="^3" class="calculator__key calculator__power"></button>
            <button type="button" value="+" class="calculator__key calculator__button"></button>
        </div>
        <!-- CALCULATOR ROW -->
        <div class="calculator__row">
            <button type="button" value="9" class="calculator__key calculator__button"></button>
            <button type="button" value="8" class="calculator__key calculator__button"></button>
            <button type="button" value="7" class="calculator__key calculator__button"></button>
            <button type="button" value="-" class="calculator__key calculator__button"></button>
        </div>
        <!-- CALCULATOR ROW -->
        <div class="calculator__row">
            <button type="button" value="6" class="calculator__key calculator__button"></button>
            <button type="button" value="5" class="calculator__key calculator__button"></button>
            <button type="button" value="4" class="calculator__key calculator__button"></button>
            <button type="button" value="*" class="calculator__key calculator__button"></button>
        </div>
        <!-- CALCULATOR ROW -->
        <div class="calculator__row">
            <button type="button" value="3" class="calculator__key calculator__button"></button>
            <button type="button" value="2" class="calculator__key calculator__button"></button>
            <button type="button" value="1" class="calculator__key calculator__button"></button>
            <button type="button" value="/" class="calculator__key calculator__button"></button>
        </div>
        <!-- CALCULATOR ROW -->
        <div class="calculator__row">
            <button type="button" value="0" class="calculator__key calculator__button"></button>
            <button type="button" value="." class="calculator__key calculator__button"></button>
            <button type="button" value="=" class="calculator__key calculator__key--equal"></button>
        </div>
    </form>
</div>
{% endhighlight %}

## CSS стили

Со стилизацией будущего калькулятора тоже проблем не должно возникнуть. Я использовал flexbox для выравнивания кнопок:

{% highlight css %}
.calculator {
    width: 250px;
    height: 350px;
    border: 2px solid black;
    margin: 100px auto 0;
    text-align: center;
    background-color: yellowgreen;
    box-shadow: 0 0 30px grey;
    border-radius: 4px;
}

.calculator__form {
    height: 100%;
    padding: 20px;
}

.calculator__row {
    margin: 10px 0;
    display: flex;
    justify-content: space-between;
}

.calculator__display {
    margin: 0 0 20px;
    width: 100%;
    border: 1px solid darkslateblue;
    padding: 4px 2px;
    text-align: right;
    font: 700 16px/1 Arial, sans-serif;
    color: darkslateblue;
    background-color: whitesmoke;
}

.calculator__key {
    width: 41px;
    height: 35px;
    cursor: pointer;
    border: none;
    transition: all .2s;
    text-transform: uppercase;
}

.calculator__key--equal {
    width: 98px;
}

.calculator__key:hover {
    background-color: yellow;
    font-weight: 700;
}

.calculator__key::-moz-focus-inner {
    border: none
}
{% endhighlight %}


## JavaScript код

Переходим к самому интересному - созданию JavaScript-кода для калькулятора. В своем примере я использовал JavaScript + jQuery.

Последний применил только из-за удобства манипуляции с DOM. Недавно узнал о существовании библиотеки [Underscore.js][1] как альтернативы jQuery, но меньшего размера. Надо опробовать Underscore.js обязательно! )

Первым делом инициализируем кнопки калькулятора. Для этого забираем значения из атрибута `value` кнопок `button` и динамически вставляем в HTML-разметку:

{% highlight javascript %}
// INIT CALC KEYS
calcKeys.each(function () {
    var current = $(this).attr('value');
    $(this).text(current);
});
{% endhighlight %}

Исходный вид калькулятора подготовили - он теперь выглядит как настоящий калькулятор! Если не принимать во внимание кошмарных цветов и их сочетания ) Ну мы не дизайнеры, нам простительно )

Теперь стоит задача - при нажатии на кнопку калькулятора чтобы ее значение появлялось в окошке последнего. Тоже ничего сложного, если подумать.

Просто нужно забрать у активной кнопки значение ее атрибута `value` и передать как значение элемента `input`.

Небольшая тонкость здесь - нужно конкатенировать текущее значение элемента `button` с текущим значением элемента `input`; иначе будет происходить простое замещение предыдущего значения элемента `input` текущим значением элемента `button`:

{% highlight javascript %}
// ADD NUMBERS TO INPUT
calcButton.on('click', function () {
    calcDisplay.val( calcDisplay.val() + $(this).attr('value') );
});
{% endhighlight %}

Полная очистка экрана калькулятора элементарно проста - достаточно при нажатии на соответствующую кнопку передать в элемент `input` пустое значение:

{% highlight javascript %}
// CLEAR INPUT
calcClear.on('click', function () {
    calcDisplay.val('');
});
{% endhighlight %}

Дальше уже немного интереснее - будем оживлять кнопку `=`. То есть - ввели в окошко калькулятора, к примеру, `2 + 3`. По нажатии на кнопку `=` в окошке должен появиться результат этой арифметической операции.

На помощь приходит функция JavaScript под названием `eval()`. На [javascript.ru][2] эта функция подробно [расписана][3].

В результате код для "оживления" кнопки `=` будет выглядеть "скромно":

{% highlight javascript %}
// SHOW RESULT
calcEqual.on('click', function () {
    calcDisplay.val( eval( calcDisplay.val() ) );
});
{% endhighlight %}

Наш калькулятор почти готов. Осталось добавить жизни к двум последним кнопкам - возведения в степень и посимвольной очистки экрана калькулятора.

Для возведения в степень воспользуемся стандартной JavaScript-библиотекой `Math` и ее методом `pow()`.

Заберем у элемента `input` его текущее значение и передадим в качестве одного из аргументов в метод `pow()`. Второй аргумент в нашем случае - это константа 3:

{% highlight javascript %}
// POWER BUTTON
calcPower.on('click', function () {
    calcDisplay.val( Math.pow( calcDisplay.val(), 3 ) );
});
{% endhighlight %}

Последний шаг к успеху создания калькулятора - это "оживление" кнопки посимвольной очистки экрана калькулятора.

В этом случае воспользуемся стандартным методом JavaScript - `substring()`. Это метод JavaScript(), который извлекает из строки подстроку и возвращает ее в виде новой строки - [почитать с примерами][4].

В качестве аргументов принимает два параметра - начальную и конечную позицию, которые выступают как начальный и конечный индекс массива. Массивом в данном случае является строка.

Функция (на кнопке посимвольной очистки) в нашем случае будет работать так - забираем у элемента `input` его текущее значение. Значение возвращается в виде строки, конечно.

Поэтому находим ее длину (`length`) и укорачиваем на один (последний) символ - `length - 1`. Таким образом мы динамически укорачиваем текущее значение в окне калькулятора на один символ.

Затем нам нужно заменить текущее значение окна калькулятора укороченным на один символ значением. Для этого берем метод `substring()` и с помощью него "обрезаем" текущую строку; этот метод возвращает "обрезанный" вариант. Нам осталось только вставить его в окно калькулятора.

Результат будет выглядеть таким образом:

{% highlight javascript %}
// BACKSPACE BUTTON
calcSpace.on('click', function () {
    calcDisplay.val( calcDisplay.val().substring(0, calcDisplay.val().length-1) );
});
{% endhighlight %}

Вот наш калькулятор и готов - ниже полный JavaScript-код:

{% highlight javascript %}
$(document).ready(function () {

    // VARIABLES
    var calc = $('.calculator');
    var calcDisplay = calc.find('.calculator__display');
    var calcKeys = calc.find('.calculator__key');
    var calcButton = calc.find('.calculator__button');
    var calcClear = calc.find('.calculator__clear');
    var calcEqual = calc.find('.calculator__key--equal');
    var calcPower = calc.find('.calculator__power');
    var calcSpace = calc.find('.calculator__backspace');

    // INIT CALC KEYS
    calcKeys.each(function () {
        var current = $(this).attr('value');
        $(this).text(current);
    });

    // ADD NUMBERS TO INPUT
    calcButton.on('click', function () {
        calcDisplay.val( calcDisplay.val() + $(this).attr('value') );
    });

    // CLEAR INPUT
    calcClear.on('click', function () {
        calcDisplay.val('');
    });

    // SHOW RESULT
    calcEqual.on('click', function () {
        calcDisplay.val( eval( calcDisplay.val() ) );
    });

    // POWER BUTTON
    calcPower.on('click', function () {
        calcDisplay.val( Math.pow( calcDisplay.val(), 3 ) );
    });

    // BACKSPACE BUTTON
    calcSpace.on('click', function () { // http://www.w3schools.com/jsref/jsref_substring.asp
        calcDisplay.val( calcDisplay.val().substring(0, calcDisplay.val().length-1) );
    });

});
{% endhighlight %}

Конечно, примеры кода из этой статьи хоть и не являются укороченными, но не дают полного представления о разрабатываемом нами калькуляторе.

Поэтому привожу ссылку на [готовый вариант калькулятора][5], который создавался в этой статье. На CodePen можно его посмотреть и разобрать детально (при желании).

Как вариант для сравнения, можно взглянуть на более сложный [пример создания калькулятора][6], на чистом JavaScript. Пример был найден мною на просторах CodePen.

## Заключение

Рассмотренный в статье пример лично для меня оказался на удивление прост - я ожидал большей (и более запутанной) кучи кода.

На этом все. В дальнейшем буду продолжать флудить на тему JavaScript, ибо для себя с удивлением обнаружил, что мне в последнее вермя доставляет удовольствие разбирать и рассматривать готовые примеры на JavaScript.

Единственное, что меня огорчает - тот факт, что они чужие )

***
[1]: http://underscorejs.org/ "Underscore.js"
[2]: https://learn.javascript.ru/ "javascript.ru"
[3]: https://learn.javascript.ru/eval "Запуск кода из строки: eval"
[4]: http://www.w3schools.com/Jsref/jsref_substring.asp "JavaScript String substring() Method"
[5]: http://codepen.io/gearmobile/pen/gMaYgE "JavaScript Calculator"
[6]: http://codepen.io/gearmobile/pen/rLOBwm "JavaScript Another Calculator"