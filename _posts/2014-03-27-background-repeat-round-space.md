---
title: "Background-repeat и его значения round и space"
layout: post
categories: css
tags: [background-repeat, round, space]
share: true
---

> Помимо хорошо известных четырех значений свойства `background-repeat` - `repeat`, `no-repeat`, `repeat-x`, `repeat-y`, в спецификации CSS3 появились еще два, с которыми я познакомился совсем недавно.

Перечислим их:

  * `background-repeat: round`
  * `background-repeat: space`

Отлично, скажете вы! Ну и что, что же это за свойства? Мало прежних четырех? Давайте разберемся сначала, что это за свойства, а уже потом будем говорить, нужны они или не нужны.

## Свойство background-repeat: repeat

Для начала посмотрим, как работает простое и привычное нам значение `repeat`:

{% highlight css %}
.rnd{
  width: 700px;
  height: 500px;
  margin: 10px;
  border: 1px solid #000;
  background-image: url(img/ChristinaVujnich.jpg);
  background-position: top left;
  background-repeat: repeat;
}
{% endhighlight %}

![Свойство background-repeat: repeat]({{site.url}}/images/uploads/2014/03/background-repeat_repeat.jpg)

Видим, как браузер аккуратно сделал все, что мы от него требовали - размножил фоновое изображение по горизонтали и по вертикали. Что не вместилось в блок, то было обрезано. Получилось несколько некрасиво; но зато - что требовали.

## Свойство background-repeat: round

В спецификации CSS3 появилось одно из двух значений свойства `background-repeat`, которое делает попытку исправить ситуацию и выполнять "заливку" фона более красиво и "интеллектуально". Это значение называется `round` - от английского округлять.

Работает оно по следующему принципу - изображение размножается по вертикали и горизонтали фона блока, как и прежде. Но при этом браузер определяет, сколько раз удалось поместить изображение в блок без обрезки (по вертикали и по горизонтали). Сколько "целых" раз удалось поместить - столько раз он и помещает. А с оставшимся пустым пространством он поступает так - растягивает изображение по вертикали и горизонтали, чтобы равномерно заполнить это пустое пространство.

Пример показан ниже:

{% highlight css %}
.rnd{
  width: 700px;
  height: 500px;
  margin: 10px;
  border: 1px solid #000;
  background-image: url(img/ChristinaVujnich.jpg);
  background-position: top left;
  background-repeat: round;
}
{% endhighlight %}

![Свойство background-repeat: round]({{site.url}}/images/uploads/2014/03/background-repeat_round.jpg)

Результат получился не слишком красивый, конечно. Но зачет - попытка сделана. А если быть более точным и без всякого "юмора", то такой способ хорошо подойдет для фоновых изображений небольшого размера.

## Свойство background-repeat: space

Еще одно значение свойства `background-repeat` из спецификации CSS3, призванное решить проблему красивого размещения фонового изображения в блоке элемента, это значение `space`.

Принцип работы этого свойства аналогичен значению `round` - браузер также считает количество целых "вхождений" изображения в фон элемента. Но вот с пустым пространством он поступает несколько иначе. Браузер равномерно распределяет его между изображениями (размер которых он оставляет неизменными).

Чтобы было понятно, о чем идет речь, посмотрите на пример ниже:

{% highlight css %}
.rnd{
  width: 700px;
  height: 500px;
  margin: 10px;
  border: 1px solid #000;
  background-image: url(img/ChristinaVujnich.jpg);
  background-position: top left;
  background-repeat: space;
}
{% endhighlight %}

![Свойство background-repeat: space]({{site.url}}/images/uploads/2014/03/background-repeat_space.jpg)

Мною намеренно были изменены размер блока, для которого "прописывалось" фоновое изображение; и размер самого изображения также. Все было сделано с целью более наглядного представления, как работает значение `space` для свойства `background-repeat`.

На рисунке выше хорошо видно, как браузер равномерно распределил пустое пространство по вертикали и горизонтали между изображениями.

## Значения Round & Space - поддержка браузерами

В заключение осталось упомянуть последнее - какими браузерами поддерживаются оба значения свойства `background-repeat`. Похвастаться особо нечем - только два браузера на момент написания этой статьи поддерживают `space` и `round`. Первый - это Google Chrome начиная с `v.32`. А вот второй браузер, который может похвастаться (держитесь крепче за стул!) - это Internet Explorer v10.

## Поддержка с помощью Modernizr

В библиотеку Modernizr включена (благодаря ходатайству Louis Lazaris) поддержка значений `round` и `space` CSS-свойства `background-repeat` с помощью соответствующих классов `bgrepeatspace` и `bgrepeatround`. Поэтому, теперь можно использовать эту библиотеку для определения возможности поддержки в браузерах.

Например, таким кодом:

{% highlight css %}
.element {
  width: 550px;
  height: 400px;
  background: transparent url(bg.jpg) repeat 0 0; /* for all browsers */
}

.bgrepeatspace .element {
  background-repeat: space; /* for supporting browsers */
}
{% endhighlight %}

## Заключение

Вот, в принципе, и все по значениям `round` и `space` свойства `background-repeat`. В статье активно использовались мысли (и даже код, когда шла речь о Modernizr) из источника:

[CSS3′s ‘space’ and ‘round’ Values for background-repeat][1]

На этом все.

---

[1]: http://www.impressivewebs.com/space-round-css3-background/ "CSS3′s ‘space’ and ‘round’ Values for background-repeat"
