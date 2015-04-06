---
title: "Цикл for в Sass"
layout: post
categories: css
tags: [sass, for]
share: true
---

> Очень краткий пример работы с циклом `for` в препроцессоре Sass.

С чего вдруг мне приспичило воспользоваться циклом в препроцессоре? Все, как всегда, просто - в предыдущей статье, посвященной плагину Smooth Scroll ([Плагин Smooth Scroll][1]), мне потребовался создать пример разметки HTML-документа с заголовками всех уровней, с первого (h1) до шестого (h6). Все бы ничего, но вручную создавать стили для заголовков всех уровней как-то утомительно.

## HTML-разметка для цикла for

Вот я и озаботился задачей автоматизировать этот процесс, через цикл. Для этой цели я использовал цикл `for`. Упростил пример, выкинув параграфы и оставив только заголовки всех уровней:

{% highlight html %}
<div class="wrapper">
  <h1>header 1</h1>
  <h2>header 2</h2>
  <h3>header 3</h3>
  <h4>header 4</h4>
  <h5>header 5</h5>
  <h6>header 6</h6>
</div>
{% endhighlight %}

## Базовые CSS-стили

Затем пропишу основные стили для этой разметки:

{% highlight css %}
$color: #778899;
$percent: 5%;
$percentStep: 5;
$fontSize: 76px;
$fontSizeStep: 10;

.wrapper{
  width: 60%;
  margin: 5% auto 0;
  text-align: center;
}

h1,h2,h3,h4,h5,h6{
  font-family: Arial, sans-serif;
  text-transform: capitalize;
  margin-bottom: 4%;
}
{% endhighlight %}

## Использую цикл for в Sass

Теперь у меня стоит задача "покрасить" все заголовки в оттенки цвета, указанного в переменной `$color: #778899;`. Для создания оттенков воспользуюсь функцией `lighten()` из препроцессора Sass.

Цвет будет меняться с шагом в 5% (`$percentStep: 5;`):

{% highlight css %}
h1{
  color: lighten($color,5%);
}

h2{
  color: lighten($color,10%);
}

h3{
  color: lighten($color,15%);
}
...
{% endhighlight %}

Также будет изменяться размер шрифта (*кегль*) в заголовках уровней с первого (`h1`) до шестого (`h6`), с шагом 10px (`$fontSizeStep: 10`):

{% highlight css %}
h1 {
  font-size: 76px;
}

h2 {
  font-size: 66px;
}

h3 {
  font-size: 56px;
}
...
{% endhighlight %}

Как видим, задача и вправду не для ленивых - это же надо тупо вбивать столько значений! Но мне поможет Sass и его циклы, а точнее - цикл `for`.

Для этого создаю такую конструкцию цикла `for`:

{% highlight css %}
@for $i from 1 through 6 {
  h#{$i}{
    color: lighten($color,$percent);
    font-size: $fontSize;
    $percent: $percent + $percentStep;
    $fontSize: $fontSize - $fontSizeStep;
  }
}
{% endhighlight %}

Небольшая расшифровка приведенного выше цикла. В данном случае используется цикл `for`, в котором счетчик `$i` изменяет свое значение в диапазоне от 1 до 6 включительно. Конструкция `#{$i}` называется экранированием в Sass и служит для того, чтобы значение счетчика `$i` подставилось в коде "как есть", в виде текста.

В результате получается такой вывод:

  * h1
  * h2
  * h3
  * h4
  * h5
  * h6

Далее идут CSS-правила с использованием функции `lighten()` препроцессора Sass и переменных `$color`, `$percent`, `$fontSize`. Последние две строки производят увеличение значения переменных на указанный шаг:

{% highlight css %}
$percent: $percent + $percentStep;
$fontSize: $fontSize - $fontSizeStep;
{% endhighlight %}

Приведенный выше SCSS-код скомпилируется в готовый CSS-код подобного вида:

{% highlight css %}
h1 {
  color: #8695a4;
  font-size: 76px;
}

h2 {
  color: #94a2af;
  font-size: 66px;
}

h3 {
  color: #a3aeba;
  font-size: 56px;
}

h4 {
  color: #b1bbc5;
  font-size: 46px;
}

h5 {
  color: #c0c8d0;
  font-size: 36px;
}

h6 {
  color: #ced5db;
  font-size: 26px;
}
{% endhighlight %}

Смотрим результат в браузере и радуемся успеху:

![Результат работы цикла for в Sass]({{site.url}}/images/uploads/2014/07/sass_cycle.jpg)

## Полный код примера цикла for в Sass

Полный код рассмотренного примера создания цикла `for` в Sass приведен ниже:

{% highlight html %}
<div class="wrapper">
  <h1>header 1</h1>
  <h2>header 2</h2>
  <h3>header 3</h3>
  <h4>header 4</h4>
  <h5>header 5</h5>
  <h6>header 6</h6>
</div>
{% endhighlight %}

{% highlight css %}
@import "compass/reset";

$color: #778899;
$percent: 5%;
$percentStep: 5;
$fontSize: 76px;
$fontSizeStep: 10;

.wrapper{
  width: 60%;
  margin: 5% auto 0;
  text-align: center;
}

h1,h2,h3,h4,h5,h6{
  font-family: Arial, sans-serif;
  text-transform: capitalize;
  margin-bottom: 4%;
}

@for $i from 1 through 6 {
  h#{$i}{
    color: lighten($color,$percent);
    font-size: $fontSize;
    $percent: $percent + $percentStep;
    $fontSize: $fontSize - $fontSizeStep;
  }
}
{% endhighlight %}

Скомпилированный в CSS-код результат нашего кодинга:

{% highlight css %}
.wrapper {
  width: 60%;
  margin: 5% auto 0;
  text-align: center;
}

h1, h2, h3, h4, h5, h6 {
  font-family: Arial, sans-serif;
  text-transform: capitalize;
  margin-bottom: 4%;
}

h1 {
  color: #8695a4;
  font-size: 76px;
}

h2 {
  color: #94a2af;
  font-size: 66px;
}

h3 {
  color: #a3aeba;
  font-size: 56px;
}

h4 {
  color: #b1bbc5;
  font-size: 46px;
}

h5 {
  color: #c0c8d0;
  font-size: 36px;
}

h6 {
  color: #ced5db;
  font-size: 26px;
}
{% endhighlight %}

На этом все.

---

 [1]: http://localhost:7788/third/?p=1527 "Плагин Smooth Scroll"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/07/sass_cycle.jpg
