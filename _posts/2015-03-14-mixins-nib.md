---
title: 'Миксины Nib'
author: gearmobile
layout: posts
---
Начнем с небольшой темки, которая может даже и не стоит того, чтобы о ней писать. Но на момент моего знакомства с ней у меня возникла мысль - вот неплохо бы описать этот случай. Потом, когда я уже был достаточно знаком с темой, желание и потребность вроде как и пропала. Но, когда я снова вернулся к ней, то все же решил - стоит!

О чем будет речь? О миксинах библиотеки Nib. Ранее я уже писал о том, как подключать эту библиотеку в свой проект. Ничего сложного в этом нет - достаточно установить Nib и подключить ее в проект.

Но вот вопрос о миксинах этой библиотеки - это отдельный вопрос. Дело в двух моментах - размере библиотеки и документации к ней.

**Во-первых** - Nib гораздо меньше, чем Compass (это чтобы было, с чем сравнивать). Compass больше, тщательнее сработан - в этой библиотеке есть миксины практически на все случаи жизни. У Nib миксинов меньше, ощутимо меньше.

На это можно ответить вполне резонно. Первое - из личного опыта, на своей практике из всего большого многообразия миксинов Compass я использовал только 10 штук (максимум). Второе - написать миксин на Stylus не просто, а очень просто! Так что, если возникает в этом необходимость - никаких проблем в создании пользовательского миксина не может быть.

**Вторая проблема** с Nib более существена и неприятна, скажем так. Заключается она в отсутствии хорошо сделанной документации к библиотеке Nib. То есть, есть официальный сайт проекта Nib, есть репозиторий на GitHub. Но вот такой хорошо оформленной документации, как у Compass, вы не найдете.

Именно поэтому у меня и возникла мысль, перевоплотившаяся в желание написать маленькое пособие для небольшой доли миксинов, которые доступны в Nib.

### Size

Миксин для задания размеров элементам `display: block` или `display: inline-block`. Преимущество у данного миксина - в краткости его написания. Не нужно писать - `width: 20px; height: 20px;`, достаточно написать одну строчку:

{% highlight css %}
.block
	size 20px 30px
{% endhighlight %}

{% highlight css %}
.block
	width: 20px;
	height: 30px;
{% endhighlight %}

{% highlight css %}
.block
	size 20px
{% endhighlight %}

{% highlight css %}
.block
	width: 20px;
	height: 20px;
{% endhighlight %}

### Overflow

Миксин для задания свойства `text-overflow: ellipsis`. Полезный миксин, которые реально может помочь в написании одной строки стилей вместо трех правил.

{% highlight css %}
.block
	overflow ellipsis
{% endhighlight %}

{% highlight css %}
.block
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
{% endhighlight %}

### Absolute/Fixed/Relative

Миксин для генерирования CSS-свойства `position: absolute`, `position: fixed`, или `position: relative`. Этот миксин очень похож на миксин `size` - все преимущество его использования только в краткости записи.

{% highlight css %}
.block
  absolute top left
{% endhighlight %}

{% highlight css %}
  position: absolute;
  top: 0;
  left: 0;
{% endhighlight %}

{% highlight css %}
.block
  absolute top 20px left 30px

{% highlight css %}
.block
  position: absolute;
  top: 20px;
  left: 30px;
{% endhighlight %}

{% highlight css %}
.block
  absolute bottom 20px right 30px
{% endhighlight %}

{% highlight css %}
.block
  position: absolute;
  bottom: 20px;
  right: 30px;
{% endhighlight %}

{% highlight css %}
.block
  relative top 10px left 20px
{% endhighlight %}

{% highlight css %}
.block
  position: relative;
  top: 10px;
  left: 20px;
{% endhighlight %}

{% highlight css %}
.block
  fixed top 10px left 2%
{% endhighlight %}

{% highlight css %}
.block
  position: fixed;
  top: 10px;
  left: 20px;
{% endhighlight %}

### Border

Миксин для генерирования CSS border: 1px solid color. Достаточно бесполезный миксин, так как проще и быстрее воспользоваться shortcut'ом `bd+` из Emmet.

{% highlight css %}
.block
  border #800
{% endhighlight %}

{% highlight css %}
.block
  border: 1px solid #800
{% endhighlight %}

### Clearfix()

Миксин для генерации `clearfix`. У `jeet.gs` есть свой миксин `cf()` для генерации `clearfix`. Однако, миксин `clearfix()` имеет более понятное название, говорящее - что этот миксин делает. Поэтому использование этого миксина более логичное - читая код, можно сразу сказать, что этот миксин делает.

### Функция rgba()

Если быть точным, функция rgba() не относится к миксинам библиотеки Nib. Это функция препроцессора Stylus. И задача ее - преобразование значения цвета в формате HEX в формат RGBA(). Достаточно бесполезная функция, если только кодер не привык писать значения цветов в RGBA-формате.

{% highlight css %}
.block
  color rgba(#ff0000, .8)
{% endhighlight %}

{% highlight css %}
.block
  color: rgba(255, 0, 0, 0.9);
{% endhighlight %}

### Background

Вот этот миксин является действительно полезным - благодаря краткости записи и результату генерации этого миксина. Как уже можно догадаться, этот миксин генерирует *линейный градиент*. Направление градиента управляется служебным словом, стоящим вначале миксина - `top`, `left`, `right`, `bottom`.

{% highlight css %}
.block
  background linear-gradient(top,#f00,#0f0)
{% endhighlight %}

Миксин для генерации радиального градиента - очень похож на линейный градиент. Разница только в некоторых моментах:

{% highlight css %}
.block
  background radial-gradient(center,#f00 30%, #fff 31%)
{% endhighlight %}

### Box-sizing

Еще один полезный миксин - для генерации CSS-свойства box-sizing: border-box. Что это за свойство, говорить не приходиться.

{% highlight css %}
.block
  box-sizing: border-box
{% endhighlight %}

{% highlight css %}
.block {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
{% endhighlight %}

### Image

Миксин для генерации CSS-свойства `background-image`. Генерируются два свойства - для нормального разрешения, и для Retina. Для этого необходимо подготовить **два варианта изображений**, как было сказано выше - тогда миксин сработает.

Первое изображение - *нормального размера* для нормального разрешения. Второе изображение - *увеличенная вдвое* версия нормального изображения, для Retina-экранов (это версия `@2x`).

{% highlight css %}
.block
  image 'images/background.jpg'
{% endhighlight %}

{% highlight css %}
.block {
  background-image: url("images/background.jpg");
}

@media all and (-webkit-min-device-pixel-ratio: 1.5) {
  .block {
    background-image: url("images/background@2x.jpg");
    background-size: auto auto;
  }
}
{% endhighlight %}
