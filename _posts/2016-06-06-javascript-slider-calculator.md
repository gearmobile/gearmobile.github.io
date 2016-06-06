---
title: "JavaScript - Slider Calculator"
layout: post
categories: javascript
tags: [javascript, slider, calculator]
share: true
---

Пример создания калькулятора на основе HTML-элемента `input type="range"`. Это слайдер, у которого можно плавно изменять значения при помощи ползунка. Текущее значение хранится в атрибуте `value` данного элемента.

На этом принципе и основана работа калькулятора, который рассмотрим ниже.

Что будет считать калькулятор? В качестве примера - сумму чаевых в кафе. Есть основная сумма ($), задается процент (%) чаевых для основной суммы.

Нужно посчитать результирующую сумму ($).

## HTML разметка

Разметка калькулятора основана на элементах `form`, `input type="text"`, `input type="range"`. Она простая и представлена ниже:

{% highlight html %}
<div class="wrapper">
    <h1 class="wrapper__title">javascript slider calculator</h1>
    <form class="calculator">
        <div class="calculator__row">
            <label for="bill">enter the bill amount for your meal: $</label>
            <input type="text" id="bill" class="calculator__bill" value="5" required/>
        </div>
        <div class="calculator__row">
            <label for="tip">tip amount: <span class="tip-amount"></span></label>
            <input type="range" min="0" max="100" value="0" step="1" class="calculator__tip" id="tip" required/>
        </div>
        <div class="calculator__row">
            <h2 class="calculator__info">tip to leave: <span class="calculator__result"></span></h2>
        </div>
    </form>
</div>
{% endhighlight %}

## CSS стили

Стилизация для калькулятора также не отличается объемом и сложностью. Что-либо отмечать отдельно нет необходимости:

{% highlight css %}
.wrapper {
    width: 800px;
    margin: 50px auto 0;
    padding: 60px 30px;
    border: 1px solid #000;
}

.wrapper__title {
    text-transform: capitalize;
    margin: 0 0 40px;
}

.calculator__row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 0 30px;
}

.calculator__row:last-child {
    margin-bottom: 0;
}

.calculator__row label {
    text-transform: capitalize;
    font-weight: 700;
}

.calculator__bill {
    width: 50%;
}

.calculator__tip {
    width: 60%;
}

.calculator__info {
    text-transform: capitalize;
    margin: 0;
}
{% endhighlight %}

## JavaScript код

Функция для вычисления результирующей суммы "повешена" на элемент `input type="range"` и событие `change`.

Другими словами, при **перемещении** ползунка слайдера каждый раз будет вызываться функция и производится пересчет на основе изменившегося значения атрибута `value`.

Принцип работы функции следующий. "Забираем" значения из элементов `input type="text"` и `input type="range"`. Первое значение - эту основная сумма ($); второе значение - процент (%) от основной суммы ($).

Получаем результирующую сумму путем сложения - основной суммы ($) + процент (%) от основной суммы. Результирующий вывод **округляем** до двух значений после запятой при помощи [метода toFixed()][1].

Помимо этого, проверяем **правильность** и **наличие** ввода в поле основной суммы ($) `input type="text"`. Условие будет верным, если поле ввода окажется не **пустым** и содержащим только **цифры**:

{% highlight javascript %}
// RANGE FUNCTION
// ----------------------------------------------------------
calculatorTip.on('change', function () {

    if ( calculatorBill.val() === '' || isNaN( calculatorBill.val() ) ) {
        alert('Enter bill amount, please!')
    } else {
        amount = calculatorBill.val() * 1;
    }

    tipAmount.text( calculatorTip.val() + '%' );
    percent = calculatorTip.val() * 1;
    result = amount + amount * ( percent / 100 );
    calculatorResult.text( result.toFixed(2) + '$' );
});
{% endhighlight %}

Для "украшательства" можно создать еще одну функцию, которая будет запускаться при загрузке страницы и инициализировать значения **суммы** ($), **процентов** (%) от суммы и **результирующей** суммы ($):

{% highlight javascript %}
// INIT FUNCTION
// ----------------------------------------------------------
$(window).on('DOMContentLoaded', function () {
    tipAmount.text( calculatorTip.val() + '%' );
    amount = calculatorBill.val() * 1;
    percent = calculatorTip.val() * 1;
    result = amount + amount * ( percent / 100 );
    calculatorResult.text( result.toFixed(2) + '$' );
});
{% endhighlight %}

Весь JavaScript-код для обработки калькулятора можно представить ниже:

{% highlight javascript %}
$(document).ready( function () {


	// VARIABLES
	// ----------------------------------------------------------

	var amount, percent, result;
	var calculator = $('.calculator');
	var calculatorBill = calculator.find('.calculator__bill');
	var calculatorTip = calculator.find('.calculator__tip');
	var calculatorResult = calculator.find('.calculator__result');
	var tipAmount = calculator.find('.tip-amount');


	// INIT FUNCTION
	// ----------------------------------------------------------

	$(window).on('DOMContentLoaded', function () {
	    tipAmount.text( calculatorTip.val() + '%' );
	    amount = calculatorBill.val() * 1;
	    percent = calculatorTip.val() * 1;
	    result = amount + amount * ( percent / 100 );
	    calculatorResult.text( result.toFixed(2) + '$' );
	});


	// RANGE FUNCTION
	// ----------------------------------------------------------

	calculatorTip.on('change', function () {

	    if ( calculatorBill.val() === '' || isNaN( calculatorBill.val() ) ) {
	        alert('Enter bill amount, please!')
	    } else {
	        amount = calculatorBill.val() * 1;
	    }

	    tipAmount.text( calculatorTip.val() + '%' );
	    percent = calculatorTip.val() * 1;
	    result = amount + amount * ( percent / 100 );
	    calculatorResult.text( result.toFixed(2) + '$' );
	});

});
{% endhighlight %}

Готовый пример калькулятора-слайдера можно посмотреть **здесь** - [JavaScript Slider Calculator][2]

***

На этом все. В ближайшее время буду продолжать нести JavaScript-flood )

[1]: http://www.w3schools.com/Jsref/jsref_tofixed.asp "JavaScript toFixed() Method"
[2]: http://codepen.io/gearmobile/pen/beVNqj "JavaScript Slider Calculator"