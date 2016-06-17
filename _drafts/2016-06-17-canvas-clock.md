---
title: "JavaScript - Canvas Clock"
layout: post
categories: javascript
tags: [javascript, canvas]
share: true
---

Пример создания часов на Canvas. Снова я "подсмотрел" пример из зарубежного источника.

И снова мне захотелось его разобрать "по косточкам". Поэтому на оригинальность не претендую (*к моему сожалению*).

## HTML-разметка

Для HTML-разметки создаем элемент canvas:

{% highlight html %}
<canvas id="clock" class="clock"></canvas>
{% endhighlight %}

Затем в JavaScript-скрипте "достаем" элемент canvas и динамически задаем для него размеры `500 x 500` (мне нравится задавать их динамически):

{% highlight javascript %}
window.addEventListener( 'DOMContentLoaded', function () {

    var clock = document.querySelector('#clock').getContext('2d');
    clock.canvas.width = 500;
    clock.canvas.height = 500;

}, false);
{% endhighlight %}

## Текущее время

Создаем новый экземпляр объекта Date для того, чтобы получить текущее время:

{% highlight javascript %}
var now = new Date();
{% endhighlight %}

Затем из полученного объекта получаем значения времени - часов, минут, секунд и миллисекунд:

{% highlight javascript %}
var hours = now.getHours();
var minutes = now.getMinutes();
var seconds = now.getSeconds();
var miliSeconds = now.getMilliseconds();
{% endhighlight %}

В дополнение к этому, получим также текущую дату с учетом часового пояса и локали, в удобном для чтения человеком формате - метод [toDateString][2]:

{% highlight javascript %}
var today = now.toDateString();
// пример вывода
"Fri Jun 17 2016"
{% endhighlight %}

... и точно также - локальное время (метод [toLocaleTimeString][3]):

{% highlight javascript %}
var time = now.toLocaleTimeString();
// пример вывода
"3:34:31 PM"
{% endhighlight %}

В приведенных выше примерах (*возможного*) читателя не должен смущать американский формат даты и времени - у меня в операционной системе (Linux Mint 17.3 Cinnamon) стоит язык интерфейса и настройки USA (я предпочитаю язык оригинала):

{% highlight bash %}
nodejs|master⚡ ⇒ locale
LANG=en_US.UTF-8
LC_CTYPE=en_US.UTF-8
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
{% endhighlight %}

## hours

В canvas создаем круговую индикацию часов, минут и секунд.

Делает это будем при помощи canvas-метода `arc()`:

{% highlight javascript %}
function degreeToRadian (degree) {
    return degree * Math.PI / 180;
}

function renderTime () {

    // HOURS
    clock.beginPath();
    clock.arc( 250, 250, 200, degreeToRadian(270), degreeToRadian( hours * 15 - 90 ) );
    clock.stroke();

    // MINUTES
    clock.beginPath();
    clock.arc( 250, 250, 180, degreeToRadian(270), degreeToRadian( minutes * 6 - 90 ) );
    clock.stroke();

    // SECONDS
    clock.beginPath();
    clock.arc( 250, 250, 160, degreeToRadian(270), degreeToRadian( newSeconds * 6 - 90 ) );
    clock.stroke();

    // DATE
    clock.font = '700 24px Arial, sans-serif';
    clock.fillStyle = '#28d1fa';
    clock.fillText(today, 175, 250);

    // TIME
    clock.font = '14px Arial, sans-serif';
    clock.fillText(time, 185, 270);

}

setInterval( renderTime, 40 );
{% endhighlight %}

В приведенном выше коде остановимся на некоторых моментах.

**Первый момент** - метод `arc()` принимает аргументы для угловых значений в радианах. Для человека этот формат непривычен, так как мы пользуемся градусами.

Поэтому для удобства создадим функцию degreeToRadian, которая преобразовывает градусы в радианы.

**Второй момент** - начальный угол (точка отсчета) по стандарту canvas (я не ошибся?) - это 0. Это соответствует трем часам (15:00) на часовом циферблате.

Конечно, нас это не устраивает, поэтому смешаем начальную точку на 270 градусов (*по часовой стрелке*) так, чтобы эта точка находилась в положении 12 часов (12:00) - `degreeToRadian(270)`.

Второй аргумент - конечный угол - будет принимать значение угла динамически, из объекта `now`:

{% highlight javascript %}
var hours = now.getHours();
var minutes = now.getMinutes();
var seconds = now.getSeconds();
{% endhighlight %}

Из полученного значения нам необходимо вычесть 90 градусов потому, что хоть начальную точку мы и сместили на 270 градусов, отсчет продолжает вестись из начальной точки 0 (которая на 15:00). Почему так происходит, я так и не понял - но код работает, а это главное.

Результирующее значение умножаем на 15 или 6 для кратности - эти величины взяты чисто эмпирически. В итоге получится красивые и "смотрибельные" окружности\стрелки.

**Последний момент** - сделаем для всего этого "дела" обертку-функцию `renderTime` и "запихнем" ее в тайминговую функцию setInterval, с частотой выполнения 40 миллисекунд.

Таким образом мы оформим анимацию отрисовки окружностей\стрелок и наши часы станут настоящими (почти) часами.

Пора взглянуть по получившийся результат, ибо иначе теряется "связь с реальностью". Готовый код можно посмотреть здесь - [JavaScript Canvas Clock - Start][1].









// FILE NAME
// year-month-day-name
2013-01-15-archlinux-slim.md

// CODE SNIPPET
{% highlight javascript %}

{% endhighlight %}

// INLINE LINK
[link]( "link title")

// ANNOUNCEED LINK
[text][1]

// INLINE IMAGE
![image title]({{site.url}}/images/uploads/2015/08/images/image.jpg "image alt") 

***
[1]: // "JavaScript Canvas Clock - Start"
[2]: // "toDateString"
[3]: // "toLocaleTimeString"
