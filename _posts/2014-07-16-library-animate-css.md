---
title: "Библиотека Animate.css"
layout: post
categories: css
tags: [animate.css, css]
share: true
---

> В готовом шаблоне одного фрилансера встретил использование Animate.css - библиотеки CSS3-эффектов, созданной на самом же CSS3.

Ранее я уже встречал упоминание об этой библиотеке - [Easy CSS3 Animation with Animate.css][1]. Вот теперь пришла пора познакомиться с нею детально, что называется - на практике.

Кстати, официальная страница этого проекта расположена здесь - [Animate.css][2]. На ней можно посмотреть все возможные для этой библиотеки эффекты и подобрать подходящий в выпадающем списке.

Откровенно говоря, я приготовился к обстоятельному изучению этой библиотеки, но **все оказалось предельно просто**. Все, что нужно для подключения Animate.css - это скачать полную версию по ссылке [Download Animate.css][3]. Или же перейти на GitHub - [View on GitHub][4], чтобы выбрать сжатую (`animate.min.css`) или несжатую (`animate.css`) версию библиотеки.

## Подключение Animate.css

Для подключения библиотеки Animate.css в готовый HTML-проект, достаточно подключить в "шапке" документа скачанный CSS-файл `animate.css`:

{% highlight html %}
<head>
  <meta charset="utf-8">
  <title>Animate CSS</title>
  <link rel="stylesheet" href="css/animate.css">
  ...
</head>
{% endhighlight %}

И это все! Больше никаких действий не потребуется - все остальные манипуляции нужно выполнять в HTML-коде, **добавляя необходимые CSS-классы** из библиотеки Animate.css к нужным HTML-элементам.

## Добавление CSS-классов из Animate.css

Первое, что нужно помнить - для нужного HTML-элемента необходимо добавить **обязательный класс** `.animated`. CSS-расшифровка этого класса также предельно проста:

{% highlight css %}
.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
{% endhighlight %}

Второе - на [странице проекта][2] подбираем для себя нужный\понравившийся эффект, запоминаем имя (пусть в данном случае это будет `bounceIn`) этого эффекта и добавляем его в качестве имени класса к HTML-элементу, у которого уже есть класс `.animated` (вспоминаем основы CSS - такая конструкция называется *мультиклассовостью*):

{% highlight html %}
<h1 class="animated bounceIn">
  Animate.css
</h1>
{% endhighlight %}

Все - можно проверять работу библиотеки Animate.css.

## Использование jQuery c Animate.css

Если в проекте используется библиотека jQuery (*а она применяется почти всегда*), то применение библиотеки Animate.css еще больше упрощается, а HTML-разметка **делается семантичной**. Для этого подключаю библиотеку jQuery:

{% highlight html %}{% endhighlight %}

... и прописываю в скрипте инициализации `animate_me.js`:

{% highlight javascript %}
$(document).ready(function() {
  $('h2').addClass('animated bounceInLeft');
})
{% endhighlight %}

Вуаля - все отлично работает!

Можно немного **усложнить задачу** и добавить с помощью Jquery событие `hover` к элементу `img`, затем "повесить" на него класс анимации `rotateIn` и `animated` из библиотеки Animate.css:

{% highlight html %}
<figure>
  <img src="images/caramel.jpg" width="800" height="504" alt="Animated Image" />
</figure>
{% endhighlight %}

{% highlight javascript %}
$(document).ready(function() {
  $('figure img').hover(
  function() {
    $(this).addClass('animated rotateIn');
  },
  function() {
    $(this).removeClass('animated rotateIn');
  }
)})
{% endhighlight %}

## Управление задержкой анимации

Можно управлять **задержкой анимации** и **скоростью анимации**, изменив значения в классе `.animated`. Например, с `animation-duration: 1s` на `animation-duration: .4s;`:

{% highlight css %}
.animated {
  -webkit-animation-duration: .4s;
  animation-duration: .4s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
{% endhighlight %}

## Полный код примера на Animate.css

Полный код рассмотренного в этой статье примера привожу ниже.

{% highlight html %}
<h1 class="animated bounceIn">Animate.css</h1>
<h2>animate me with jquery!</h2>
<figure>
  <img src="images/caramel.jpg" width="800" height="504" alt="Animated Image" />
</figure>
<!--  SCRIPTS  -->
{% endhighlight %}

{% highlight css %}
$color: #778899;

h1,h2,figure{
  margin: 50px auto 0;
  text-align: center;
}

h1{
  font: normal 72px/1.3 Georgia, sans-serif;
  color: darken($color,10%);
}

h2{
  font: normal 56px/1.3 Georgia, sans-serif;
  color: lighten($color,5%);
  text-transform: capitalize;
}

figure img:hover{
  cursor: pointer;
}
{% endhighlight %}

{% highlight javascript %}
$(document).ready(function() {
  $('h2').addClass('animated bounceInLeft');
  $('figure img').hover(
  function() {
    $(this).addClass('animated rotateIn');
  },
  function() {
    $(this).removeClass('animated rotateIn');
  }
 )})
{% endhighlight %}


![Библиотека Animate.css в действии]({{site.url}}/images/uploads/2014/07/animate.css.png)

На этом все.

---

 [1]: http://www.sitepoint.com/animate-css-css3-animation/ "Easy CSS3 Animation with Animate.css"
 [2]: http://daneden.github.io/animate.css/ "Animate.css"
 [3]: https://raw.github.com/daneden/animate.css/master/animate.css "Download Animate.css"
 [4]: http://github.com/daneden/animate.css "View on GitHub"
