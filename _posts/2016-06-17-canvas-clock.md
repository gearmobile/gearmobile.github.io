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

## Время - работа с ним

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

В дополнение к этому, получим также текущую дату с учетом local time и locale, в удобном для чтения человеком формате - метод [toDateString][2]:

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

## Часы, минуты, секунды

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

Из полученного значения нам необходимо вычесть 90 градусов потому, что хоть начальную точку мы и сместили на 270 градусов, отсчет продолжает вестись из начальной точки 0 (которая на 15:00). Почему так происходит, я так и не понял - но код работает.

Результирующее значение умножаем на 15 или 6 для кратности - эти величины взяты чисто эмпирически. В итоге получится красивые и "смотрибельные" окружности\стрелки.

**Последний момент** - сделаем для всего этого "дела" обертку-функцию `renderTime` и "запихнем" ее в тайминговую функцию setInterval, с частотой выполнения 40 миллисекунд.

Таким образом мы оформим анимацию отрисовки окружностей\стрелок и наши часы станут настоящими (почти) часами.

Пора взглянуть по получившийся результат, ибо иначе теряется "связь с реальностью". Готовый код можно посмотреть здесь - [JavaScript Canvas Clock - Start][1].

Небольшое примечание - для большей наглядности примера в код были добавлены толщина линий (lineWidth), цвет линий (strokeStyle), скругление концов линий (lineCap), а также фоновая заливка (fillStyle, fillRect) всего canvas:

{% highlight javascript %}
clock.strokeStyle = '#28d1fa';
clock.lineWidth = 14;
clock.lineCap = 'round';
...
// BACKGROUND
clock.fillStyle = '#000';
clock.fillRect( 0, 0, 500, 500 );
{% endhighlight %}

И еще один момент - нужно обратить внимание на новую строку:

{% highlight javascript %}
var newSeconds = seconds + ( miliSeconds / 1000 );
{% endhighlight %}

Что она делает? Она просто получает текущее значение миллисекунд, дробит это значение на еще меньшее значение ( miliSeconds / 1000 ) и прибавляет полученный результат к значению секунд (now.getSeconds).

Зачем это делается? С одной лишь целью - сделать отрисовку секундной окружности более плавной; иначе шаг прибавления будет слишком большим и резким - получится некрасиво.

В результате код для отрисовки секундной окружности будет таким:

{% highlight javascript %}
// SECONDS
clock.beginPath();
clock.arc( 250, 250, 160, degreeToRadian(270), degreeToRadian( newSeconds * 6 - 90 ) );
clock.stroke();
{% endhighlight %}

## Часы - дата и время

Для большей красоты и информативности можно продублировать дату и время, которые можно вывести в виде текста. В этом случае нужно воспользоваться методом `fillText`, а также воспользоваться методом `font` для настройки отображения шрифта:

{% highlight javascript %}
// DATE
clock.font = '700 24px Arial, sans-serif';
clock.fillStyle = '#28d1fa';
clock.fillText(today, 175, 250);

// TIME
clock.font = '14px Arial, sans-serif';
clock.fillText(time, 185, 270);
{% endhighlight %}

Не забудем спозиционировать текст так, чтобы он нормально смотрелся и посмотрим на полученный результат - [JavaScript Canvas Clock - Date and Time][4].

## Добавляем градиент

Пример с часами можно существенно украсить, заменив простую фоновую заливку цветом на градиентную заливку.

В canvas существует два типа градиента - [линейный и радиальный][5]. В данном случае будет применяться радиальный градиент.

Градиенты в canvas добавляются совсем не так, как в CSS. Здесь это объект, у которого есть свой метод `addColorStop()`; создается градиент при помощи функции-конструктора `createLinearGradient(x,y,x1,y1)` или `createRadialGradient(x,y,r,x1,y1,r1)`.

Изменим код для создания фоновой заливки из предыдущего примера таким образом:

{% highlight javascript %}
// BACKGROUND
var gradient = clock.createRadialGradient( 250, 250, 5, 250, 250, 300 );
gradient.addColorStop( 0, '#09303a' );
gradient.addColorStop( 1, '#000' );
clock.fillStyle = gradient;
clock.fillRect( 0, 0, 500, 500 );
{% endhighlight %}

Здесь цвет, идущий (позиция 0) из центра радиального градиента - это:

{% highlight javascript %}
// BACKGROUND
...
gradient.addColorStop( 0, '#09303a' );
{% endhighlight %}

... а цвет, на котором радиальный градиент останавливается (позиция 1), это:

{% highlight javascript %}
// BACKGROUND
...
gradient.addColorStop( 1, '#000' );
...
{% endhighlight %}

Не забываем изменить строку `clock.fillStyle = '#000';` на строку `clock.fillStyle = gradient;` и посмотрим на готовый результат - [JavaScript Canvas Clock - Radial Gradient][6].

В коде выше были использованы еще два метода canvas для создания тени - `shadowBlur` (размытие тени) и `shadowColor` (цвет тени). Так результат смотрится лучше.

## canvas в image

Напоследок можно воспользоваться методом canvas под названием `toDataURL`. Этот метод может брать текущий отрисованный canvas и конвертировать его в картинку (в формате [data URI][7]).

Эту картинку можно использовать как угодно, но в том числе - вставлять на HTML-страницу. Этот подход можно применить и заменить картинкой canvas.

В результате canvas будет генерировать картинку с частотой 40 миллисекунд и с такой же частотой вставлять ее на страницу. А canvas убрать. Визуально подмены не будет заметно.

Можно проверить, правда ли на странице картинка, а не canvas. Элементарно - правый клик мыши на изображении и смотрим - в контекстном меню есть пункт "Save image as...". Будь на этом месте canvas, такого "фокуса" бы не получилось.

Делается это в угоду браузеров, которые не понимают canvas. Правда, такой способ "подвешивает" браузер со страшной силой (по крайней мере, так дело обстоит у меня). Оно и понятно (если я не ошибаюсь) - попробуйте рисовать каждые 40 миллисекунд новую картинку )

Ниже - код:

{% highlight html %}
<canvas id="clock" class="clock"></canvas>
<img src="" id="image" alt="Clock"/>
{% endhighlight %}

{% highlight css %}
.clock {
    display: none;
}
{% endhighlight %}

{% highlight javascript %}
document.querySelector('#image').src = clock.canvas.toDataURL();
{% endhighlight %}

Тут стоит заметить один важный момент - метод `toDataURL()` относится к canvas, но не к '2d'-контексту canvas'а.

Смотрим окончательный готовый результат (слегка измененный) - [JavaScript Canvas Clock - Image][8].

## P.S.
Тут вышла заминка - даже CodePen с трудом справляется с такой задачей (но если подождать, то можно увидеть).

Поэтому продублировал результат простой картинкой на странице, чтобы можно было видеть, как должно получиться:

![JavaScript Canvas Clock - Image]({{site.url}}/images/uploads/2016/06/clock-canvas.png "JavaScript Canvas Clock - Image") 

На этом все.

***

[1]: http://codepen.io/gearmobile/full/aZmzwa/ "JavaScript Canvas Clock - Start"
[2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toDateString "toDateString"
[3]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleTimeString "toLocaleTimeString"
[4]: http://codepen.io/gearmobile/full/oLzgrN "JavaScript Canvas Clock - Date and Time"
[5]: http://www.w3schools.com/canvas/canvas_gradients.asp "HTML Canvas Gradients"
[6]: http://codepen.io/gearmobile/full/oLzXbX "JavaScript Canvas Clock - Radial Gradient"
[7]: https://developer.mozilla.org/en-US/docs/Web/HTTP/data_URIs "data URIs"
[8]: http://codepen.io/gearmobile/full/bewdLK "JavaScript Canvas Clock - Image"