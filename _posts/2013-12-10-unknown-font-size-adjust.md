---
title: "Неизвестное свойство font-size-adjust"
layout: post
categories: css
tags: [font-size-adjust, css]
share: true
---

> При создании CSS-правил сталкивались ли вы с ситуацией, когда при откате (fallback) шрифта у последнего менялась пропорциональность и текст начинал выглядеть больше или меньше оригинального?

Возможно, новое замечательное свойство `font-size-adjust` из стандарта CSS3 поможет нам исправить ситуацию?

## Что делает свойство font-size-adjust

Первое, что нужно сделать - это использовать браузер Firefox для того, чтобы страница с примером отображалась правильно. Да, не Safari, а только Firefox!

Свойство `font-size-adjust` позволяет установить *оптимальный коэффициент пропорциональности* при использовании отката шрифта; если шрифт-заменитель имеет коэффициент пропорциональности, отличающийся от такого же коэффициента у главного шрифта, высота текста `x-height` (которая приблизительно равна размеру буквы `х` этого шрифта в нижнем регистре) останется неизменной.

Давайте рассмотрим рисунок ниже:

![Сравнение двух шрифтов]({{site.url}}/images/uploads/2013/12/fontsizeadjust-compare.png){:.center-image}

Как видим на рисунке, шрифт Baskerville и Georgia имеют разный *коэффициент пропорциональности*. Если произойдет замещение шрифта (с учетом того, что шрифт Baskerville является главным), то в реальности размер шрифта визуально будет больше, при одинаковой величине.

> Прим. переводчика. Еще раз - своими словами. На картинке видно, что одинаковые буквы **А** размером 320 пикселей у шрифта Baskerville и у шрифта Georgia на самом деле не одинаковые. Пропорции (о которых говорит Inyaili) букв у этих шрифтов разные! Теперь вспомним, как задается обычно шрифт в CSS-правилах.

К примеру, так:

{% highlight css %}
font: bold 12px/18px Baskerville, Georgia, serif;
{% endhighlight %}

или же так:

{% highlight css %}
font-family: Baskerville, Georgia, serif;
{% endhighlight %}

То есть, в правилах мы устанавливаем сначала главный шрифт Baskerville, который должен отображаться на странице; и вспомогательный шрифт Georgia, который должен отображаться, если браузер не найдет главный шрифт Baskerville (*это и есть откат шрифта, о котором упоминается в этой статье*). В принципе - это основы CSS .

Теперь, если принимать во внимание картинку "Сравнение двух шрифтов", то нетрудно представить, что произойдет при такой замене (откате).

Шрифт Baskerville заменится шрифтом Georgia, у обоих при этом в правилах CSS установлена одинаковая высота в 320 пикселей. Но фактическая высота (точнее - пропорции) вспомогательного шрифта Georgia больше, чем у первостепенного Baskerville! Догадайтесь, что произойдет с готовым дизайном страницы при таком откате?

При использовании свойства `font-size-adjust` значение свойства `font-size` для шрифта-заменителя будет разделено на значение `font-size-adjust`.

Не путайте свойство `font-size-adjust` со свойством `-webkit-text-size-adjust`, которое используется для подстройки размера текста на iPhone.

## Как определить значение свойства font-size-adjust

Отрывок из спецификации W3C однозначен:

> Коэффициент пропорциональности для выбранных шрифтов может быть высчитан путем сравнения одного и того же текста, но с разным значением `font-size-adjust`. Если значение свойства `font-size-adjust` подобрано верно, то при одинаковом размере шрифта текст останется неизменным для всех используемых на странице шрифтов.

Ниже я собираюсь на примере повторить вышесказанное. Давайте посмотрим на следующий код, в котором имеется параграф с двумя `span`.

{% highlight css %}
p{
	font-family: Times New Roman;
	font-size: 400px;
}

span{
	border: 1px solid #ff0000;
}

.adjust{
	font-size-adjust: 0.5;
}
{% endhighlight %}

{% highlight html %}
<p>
  <span>a</span>
  <span class="adjust">a</span>
</p>
{% endhighlight %}

Оба элемента `span` наследуют свойство `font-family` от своего родителя (элемента `p`), но второй элемент `span` также имеет еще и свойство `font-size-adjust`, заданное через класс `adjust`, значение которого выбрано наугад - `0.5`.

Если вы откроете [страницу примера][1], то взгляните на образец слева: высота красных квадратов не совпадает - значение свойства `font-size-adjust` подобрано неверно.

*У вас все квадраты на странице примера имеют одинаковую высоту? Что я говорила?*

После нескольких экспериментов я выбрала значение `0.455`. И CSS-код, создающий второй пример (расположенный на странице справа).

{% highlight css %}
p{
	font-family: Times New Roman;
	font-size: 400px;
}

span{
	border: 1px solid #00ff00;
}

.adjust{
	font-size-adjust: 0.455;
}
{% endhighlight %}

Если вы снова перейдете на [страницу примера][1], то обнаружите, что квадраты с зелеными границами имеют одинаковую высоту (*прим. переводчика - у меня они имели не совсем одинаковую высоту*) - то есть теперь у нас величина свойства `font-size-adjust` для выбранных шрифтов установлена верно.

## Пример работы свойства font-size-adjust

Для того чтобы показать, как в действительности работает свойство `font-size-adjust` для текста, мною был создан [следующий пример][1].

На этой странице `font stack` состоит из следующих шрифтов: Calibri, Lucida Sans и Verdana (именно в этом порядке шрифты должны отображаться на странице в окне браузера).

Браузер Safari генерирует эту страницу следующим образом:

![Страница с правилом font-size-adjust в браузере Safari]({{site.url}}/images/uploads/2013/12/font-size-adjust-safari.png){:.center-image}

А вот так генерирует эту страницу браузер Firefox:

![Страница с правилом font-size-adjust в браузере Firefox]({{site.url}}/images/uploads/2013/12/font-size-adjust-ff.png){:.center-image}

Как видите, браузер Firefox поддерживает одинаковую x-высоту (`x-height`) букв в зависимости от того, какой шрифт используется.

Мною не рассматривался вопрос выравнивания текста (свойство `text-align`), так как цель этой статьи была показать, каким образом свойство `font-size-adjust` может быть применено для сохранения целостности и удобочитаемости текста.

Кроме того, даже не смотря на то, что первый блок `div` имеет корректный font stack, мне пришлось вручную прописывать в правилах шрифты Lucida Sans и Verdana для остальных блоков `div`. Так что вы (и я) можете заметить разницу несмотря на то, что установлены все три шрифта.

## Заключение

Догадываюсь, что использование свойства `font-size-adjust` в конечном счете имеет только негативное применение. Но этот вопрос может быть заголовком уже другой статьи, цель же этой - просто пример использования достаточно малоизвестного CSS3-свойства, которое может быть полезным в некоторых случаях.

Признаюсь, что я не тестировала свойство `font-size-adjust` в реальных условиях, поэтому была бы рада услышать ваши отзывы по этому поводу. Данное свойство на сегодняшний день поддерживается только браузером Firefox версии от 1.0 до 3.0.

У Inyaili de Leon есть еще одна интересная статья, которую планируется мною прочитать - "Будущее CSS типографики" (The Future Of CSS Typography) на малоизвестном ресурсе для дизайнеров Smashing Magazine.

> Примечание переводчика: интересная, как и всегда, у девушки получилась статья. Для меня свойство `font-size-adjust` вообще было открытием. Помимо этого, есть масса других статей (*в том числе русскоязычных*) на тему `font-size-adjust`, но эта мне показалась самой лучшей, так как автор не лениться пробовать на практике те вопросы, которые описывает в статье. Сделал перевод в меру своих сил, поэтому могут быть неточности, конечно.

Оригинал статьи расположен по адресу - "[The Little Known font-size-adjust CSS3 Property][2]".

---


[1]: http://webdesignernotebook.com/examples/font-size-adjust-test.html "Example Font Size Adjust"
[2]: http://webdesignernotebook.com/css/the-little-known-font-size-adjust-css3-property/ "The Little Known font-size-adjust CSS3 Property"
