---
title: "Слайдер Elastislide"
layout: post
categories: javascript
tags: [elastslide, javascript]
share: true
---

> Обзор слайдера Elastislide типа Carousel, созданного под библиотеку jQuery.

Слайдер адаптивный, меняет свои размеры в зависимости от размера окна браузера. В качестве элементов управления применяются только кнопки перемотки вперед и назад. Кнопки генерируются скриптом Elastislide автоматически. Кроме этого, никаких других элементов управления не имеет.

## Подключение скрипта Elastislide

Для подключения скрипта к проекту необходимо выполнить несколько шагов. Первое, нужно создать HTML-разметку:

{% highlight html %}
<ul id="elastic" class="elastislide-list">
  <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 1"></a></li>
  <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 2"></a></li>
  <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 3"></a></li>
  <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 4"></a></li>
  <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 5"></a></li>
</ul>
{% endhighlight %}

Обязательное условие - нужно применить к списку идентификатор (с произвольным именем) и класс `elastislide-list`, на который будут "вешаться" CSS-стили. А так видим, что HTML-разметка минималистская, все отлично.

Переходим на [официальную страницу Elastislide][1] и скачиваем оттуда архив с исходниками (кнопка "Download Source").

Распаковываем архив и видим несколько папок и четыре HTML-файла с примерами работы слайдера Elastislide. Можно полюбоваться, какую красоту создает скрипт Elastislide.

Из распакованного архива потребуются не все файлы, а только некоторые из них.

## Подключаем JS-файлы

Из папки JS распакованного архива забираем все три js-файла и подключаем их следующим образом:

* файл `modernizr.custom.17475.js` подключаем в head HTML-документа:

{% highlight html %}
<script src="js/modernizr.custom.17475.js"></script>
{% endhighlight %}

* файлы `jquery.elastislide.js`, `jquerypp.custom.js`, `jquery-1.8.2.min.js` подключаем в теле HTML-документа, перед закрывающим тегом `</body>`:

{% highlight html %}
<script type="text/javascript" src="js/jquery-1.8.2.min.js"></script>
<script type="text/javascript" src="js/jquerypp.custom.js"></script>
<script type="text/javascript" src="js/jquery.elastislide.js"></script>
{% endhighlight %}

Конечно, библиотеку jQuery можно подключать не локально, а через любой из CDN'ов - это кому как нравиться. На оф. сайте в качестве примера так и делается. jQuery используется версии 1.8.2 - я ее тоже использовал; более поздние версии не проверял на работоспособность с Elastislide.

* там же создаем еще один js-файл, в котором инициализируем скрипт Elastislide и пропишем настройки для него (если они понадобятся):

{% highlight html %}
<script type="text/javascript">
  $('#elastic').elastislide();
</script>
{% endhighlight %}

## Подключение CSS-стилей

Остался еще один файл, который нужно подключить в проект - это готовые CSS-стили "от автора", чтобы слайдер Elastislide заработал. Забираем из папки CSS распакованного архива CSS-файл `elastislide.css` и подключаем его в head HTML-документа:

{% highlight html %}
<link rel="stylesheet" type="text/css" href="css/elastislide.css" />
{% endhighlight %}

Остальные два файла `custom.css` и `demo.css` в папке CSS нам не нужны - они созданы автором скрипта для презентационных целей в примерах.

Итоговая картина подключения JS-скриптов, CSS-файла и HTML-разметки будет выглядеть следующим образом:

{% highlight html %}
<head>
  <meta charset="utf-8">
  <title>Elastislide</title>
  <link rel="stylesheet" type="text/css" href="css/elastislide.css">
  <script src="js/modernizr.js"></script>
</head>

<body>

  <ul id="elastic" class="elastislide-list">
    <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 1"></a></li>
    <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 2"></a></li>
    <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 3"></a></li>
    <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 4"></a></li>
    <li><a href="#"><img src="http://placehold.it/200x100" alt="Elastic 5"></a></li>
  </ul>

  <script type="text/javascript" src="js/jquery-1.8.2.min.js"></script>
  <script type="text/javascript" src="js/jquerypp.js"></script>
  <script type="text/javascript" src="js/jquery.elastislide.js"></script>

  <!-- Кастомный скрипт для Elastislide -->
  <script type="text/javascript">
    $('#elastic').elastislide();
  </script>

</body>
{% endhighlight %}

Как результат успешного подключения всех файлов смотрим на картинку:

![Запущенный слайдер Elastislide]({{site.url}}/images/uploads/2014/06/elastislide_ready-slider.jpg)

Дальше уже можно смело редактировать файл `elastislide.css` для того, чтобы "подогнать" его под текущий дизайн страницы.

На этом все.

---

 [1]: http://tympanus.net/codrops/2011/09/12/elastislide-responsive-carousel/ "Elastslide"
