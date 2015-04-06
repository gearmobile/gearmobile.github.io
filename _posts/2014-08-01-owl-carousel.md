---
title: "Слайдер Owl Carousel"
layout: post
categories: javascript
tags: [owl carousel, javascript]
share: true
---

> Встретил на Google+ упоминание о плагине под jQuery для создания карусели - OWL Carousel.

Попробовал с ним разобраться и посмотреть примеры создания слайдеров на официальной странице. Могу сказать, что я впечатлен данным скриптом и его возможностями. Слайдер адаптивный, имеет множество настроек, обладает хорошими эффектами "из коробки". Мое личное мнение - отличный выбор для применения на практике!

Официальная страница проекта располагается здесь - [OWL Carousel][1]. Стабильная версия скрипта на данный момент - `v1.3.2`, но на странице упоминается о версии `2.0.0-beta`. Для своей работы плагин требует библиотеки jQuery версии не ниже `1.7`.

Ниже я попробую создать простой вариант карусели с помощью плагина OWL Carousel. Более интересные и продвинутые варианты, я думаю, показывать не имеет смысла. По той простой причине, что разобравшись с базовым вариантом, всегда можно его улучшить. И для этой цели как ничто лучше подойдут примеры на официальной странице - [Demo][2] и [More Demo][3]. Стоит сказать, что для себя я увидел там готовые решения практически на все случаи жизни.

## Подключение OWL Carousel

Для подключения плагина OWL Carousel к готовому проекту необходимо получить архив плагина с официальной страницы - [OWL Carousel][1] или с GitHub - [OwlCarousel][4]. В архиве имеется все, что необходимо - библиотека jQuery, плагин `owl.carousel.min.js`, готовые CSS-стили для карусели. Ничего сложного или необычного в подключении плагина OWL Carousel нет - все стандартно.

HTML-разметка и подключение скрипта будут выглядеть следующим образом:

{% highlight html %}
<ul id="carousel" class="owl-carousel carousel">
  <li><img src="images/owl1.jpg" width="300" height="200" alt="Owl_1" /></li>
  <li><img src="images/owl2.jpg" width="300" height="200" alt="Owl_2" /></li>
  <li><img src="images/owl3.jpg" width="300" height="200" alt="Owl_3" /></li>
  <li><img src="images/owl4.jpg" width="300" height="200" alt="Owl_4" /></li>
  <li><img src="images/owl5.jpg" width="300" height="200" alt="Owl_5" /></li>
  <li><img src="images/owl6.jpg" width="300" height="200" alt="Owl_6" /></li>
  <li><img src="images/owl7.jpg" width="300" height="200" alt="Owl_7" /></li>
  <li><img src="images/owl8.jpg" width="300" height="200" alt="Owl_8" /></li>
</ul>
<!--  SCRIPTS  -->
{% endhighlight %}

В `head` подключаются две готовых CSS-таблицы из архива - `owl.carousel.css` и `owl.theme.css`. Таблица `style.css` - опциональная, для настройки плагина под конкретные условия.

Тип HTML-элементов для создания разметки слайдера, по большому счету, не имеет особого значения, так как скрипт OWL Carousel умеет работать со всеми типами. Главное, чтобы у блока-обертки имелся обязательный класс `owl-carousel`, к которому будет производиться привязка стилей из файла `owl.carousel.css`.

В конце тела `body` документа подключаются библиотека jQuery, скрипт плагина OWL Carousel и файл настроек данного скрипта.

Базовая конфигурация js-файла `settings.js` выглядит следующим образом:

{% highlight javascript %}
$(document).ready(function() {
  $("#carousel").owlCarousel();
});
{% endhighlight %}

Все, можно смотреть на готовый (*слегка подредактированный*) результат:

![Базовый вариант слайдера OWL Carousel]({{site.url}}/images/uploads/2014/08/owl_carousel-base.jpg)

## Настройка плагина OWL Carousel

Скрипт OWL Carousel имеет большое количество настроек, которые добавляются или убираются в файле настроек. Ссылка на страницу с полным списком настроек располагается здесь - [Customizing OWL Carousel][6].

К примеру, переменная `items` задает количество одновременно показываемых в слайдере изображений:

{% highlight javascript %}
items: 5
{% endhighlight %}

Переменные `itemsDesktopSmall`, `itemsTablet`, `itemsTabletSmall`, `itemsMobile` устанавливают количество одновременно отображаемых изображений в зависимости от размера окна браузера. Например, запись вида `itemsDesktop: [1199,4]` "говорит" браузеру, что при размере окна **меньше или равному** 1199px следует отображать одновременно только четыре изображения:

{% highlight javascript %}
itemsDesktop: [1199,4]
{% endhighlight %}

Переменная `singleItem` устанавливает, отображать ли только одно изображение в слайдере или несколько:

{% highlight javascript %}
singleItem: false
{% endhighlight %}

Переменные `navigation` и `pagination` управляют возможностью включения или выключения навигации\пагинации у слайдера:

{% highlight javascript %}
navigation: true,
pagination: true
{% endhighlight %}

Автоматическая прокрутка изображений в слайдере включается с помощью переменной `autoPlay`:

{% highlight javascript %}
autoPlay: true
{% endhighlight %}

Имеются множество других настроек плагина OWL Carousel, с которыми можно легко разобраться на официальной странице. Все перечислять здесь я не буду.

## Варианты слайдера OWL Carousel

Стоит "побродить" по странице с демонстрационными примерами работы плагина OWL Carousel. Там есть на что посмотреть и что подобрать для себя.

Мне понравились примеры создания слайдеров - [Lazy Load][7] и [Auto Height][8].

Наиболее интересные (*для меня*) примеры расположены в списке со ссылками.

К примеру, по ссылке [CSS3 Transitions][9] располагается образец слайдера с эффектом перехода, основанном на CSS3-свойстве transition. Более того, из выпадающего списка можно прямо на странице подобрать себе подходящий эффект - своеобразный конструктор получается:

![Слайдер OWL Carousel с эффектом transition]({{site.url}}/images/uploads/2014/08/owl_carousel-transitions.jpg)

Или пример создания слайдера с расположенной вверху полосой progress bar - [Progress Bar][10].

## Заключение

Плагин OWL Carousel мне понравился и я буду стараться применять его на практике, при верстке страниц.

---

 [1]: http://owlgraphic.com/owlcarousel/ "OWL Carousel"
 [2]: http://owlgraphic.com/owlcarousel/#demo "Demo"
 [3]: http://owlgraphic.com/owlcarousel/#more-demos "More Demo"
 [4]: https://github.com/OwlFonk/OwlCarousel "OwlCarousel"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/08/owl_carousel-base.jpg
 [6]: http://owlgraphic.com/owlcarousel/#customizing "Customizing OWL Carousel"
 [7]: http://owlgraphic.com/owlcarousel/demos/lazyLoad.html "Lazy Load"
 [8]: file:///media/aaron/small_flash/source/owl.carousel/demos/autoHeight.html "Auto Height"
 [9]: file:///media/aaron/small_flash/source/owl.carousel/demos/transitions.html "CSS3 Transitions"
 [10]: http://owlgraphic.com/owlcarousel/demos/progressBar.html "Progress Bar"
