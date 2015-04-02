---
title: "Foundation - создаем кнопки"
layout: post
categories: css
tags: [foundation, css]
share: true
---

> Продолжение обзора фреймворка Foundation, в котором приступим к практической части и научимся создавать кнопки на этом фреймворке.

Почему сразу такой быстрый переход к практике? Я сам всегда так учился всему и считаю, что это наилучший способ научиться что-либо делать. Нежели долго и нудно жевать сопли теории, чтобы когда-нибудь перейти к практике. Остальные основы Foundation я буду изучать с вами в дальнейшем, шаг за шагом.

Итак, в [первой части знакомства с Foundation][1] я с вами установил фреймворк Foundation c поддержкой Sass/Compass под операционной системой Linux Mint 17 и подготовил его к работе. Давайте откроем созданный утилитой foundation индексный файл index.html и рассмотрим его содержимое. "Шапка" `head` этого HTML-документа не представляет из себя что-то особенное, кроме двух строк:

{% highlight html %}
<link rel="stylesheet" href="css/app.css" />
<script src="bower_components/modernizr/modernizr.js"></script>
{% endhighlight %}

В первой строке производится подключение файла CSS-стилей `app.css`, который служит для создания пользовательских CSS-правил. Другими словами, фреймворк Foundation представляет из себя набор готовых CSS-стилей (на то он и фреймворк). Но не всегда готовые CSS-стили отвечают конкретным требованиям дизайна страницы. Чтобы изменить или переопределить готовые CSS-стили фреймворка Foundation, служит таблица стилей `app.css` - именно туда нужно вносить свои собственные CSS-правила.

Вторая строка - это подключение библиотеки Modernizr и больше тут сказать нечего.

Если заглянуть в самый конец HTML-документа, то увидим три строки подключения js-скриптов перед закрывающим тегом `</body>`:

{% highlight html %}
<script src="bower_components/jquery/dist/jquery.min.js"></script>
<script src="bower_components/foundation/js/foundation.min.js"></script>
<script src="js/app.js"></script>
{% endhighlight %}

Ситуация здесь почти такая же, как и с "шапкой" head документа. Подключается библиотека jQuery (куда же без нее?), коллекция готовых js-скриптов от Foundation `foundation.min.js` для создания разнообразных меню, табов и тому подобное. Скрипт `app.js` служит для тех же целей, что и таблица стилей `app.css` - для внесения пользовательских изменений.

Между тегами `<body></body>` размещено содержимое документа в виде CSS-сетки Grid, к которой я вернусь немного позже. Сейчас я произвожу очистку этого содержимого, чтобы писать в нем свой собственный HTML-код.

## Кнопки на Foundation

Создание кнопок на фреймворке Foundation **занятие малоутомительное**. Для этой цели используется тег `a`, которому присваивается имя готового CSS-класса `.button`. Помимо этого, имеются три или четыре группы классов, с помощью которых можно создавать различные варианты кнопок - разного цвета, формы и назначения.

Кнопки, созданные на Foundation c помощью предопределенных классов, имеют полностью готовый вид, вплоть до CSS-свойства transition.

### Обычная кнопка на Foundation

Как я уже упоминал выше, для создания кнопки под Foundation достаточно присвоить тегу `a` имя готового класса `.button`. Давайте так и сделаем:

{% highlight html %}
<a href="#" class="button">read more</a>
{% endhighlight %}

![Обычная кнопка на Foundation]({{site.url}}/images/uploads/2014/06/foundation_simple_button.png)

Все очень просто. Готовый результат можно посмотреть в браузере. Я же перейду к более интересному вопросу создания различных модификаций (вариантов) стандартной кнопки `.button`.

### Кнопки разных размеров

Начнем с группы классов, служащих для создания кнопок различных размеров. В этой группе имеются четыре класса для создания четырех размеров кнопок:

* `.tiny` - крошечная кнопка
* `.small` - маленькая кнопка
* `.medium` - средняя кнопка
* `.large` - большая кнопка

В качестве примера приведу ниже HTML-код создания таких кнопок:

{% highlight html %}
<a href="#" class="button tiny">tiny</a>
<a href="#" class="button small">small</a>
<a href="#" class="button medium">medium</a>
<a href="#" class="button large">large</a>
{% endhighlight %}

![Кнопки разных размеров на Foundation]({{site.url}}/images/uploads/2014/06/foundation_sizes_of_buttons.png)

Как видно из приведенного выше кода, используется мультиклассовость - добавление к классу `.button` любого из классов размера кнопки - `.tiny`, `.small`, `.medium`, `.large`. Смешение CSS-правил обоих классов дает в результате нужный вид кнопки. Впрочем, все это должно быть известно из основ CSS.

### Скругленные кнопки на Foundation

В фреймворке имеются два готовых класса для создания скругленной формы у кнопки. Первый класс - `.radius` задает радиус скругления углов у кнопки. Второй радиус `.round` создает круглую кнопку.

* `.radius` - радиус ускругления углов у кнопки
* `.round` - круглая кнопка

HTML-код создания таких кнопок показан ниже:

{% highlight html %}
<a href="#" class="button radius">radius</a>
<a href="#" class="button round">round</a>
{% endhighlight %}

![Скругленные кнопки на Foundation]({{site.url}}/images/uploads/2014/06/foundation_rounded_buttons.png)

### Информационные кнопки на Foundation

Не знаю, точно ли такое название отражает предназначение подобных кнопок, но на другом фреймворке - Twitter Bootstrap как имеется такое название для этих кнопок, поэтому решил и в Foundation назвать их также.

* `.secondary` - обычная кнопка
* `.success` - кнопка, информирующая об успешном выполнении задачи
* `.alert` - кнопка предупреждения о чем-либо

HTML-код для создания информационных кнопок:

{% highlight html %}
<a href="#" class="button secondary">secondary</a>
<a href="#" class="button success">success</a>
<a href="#" class="button alert">alert</a>
{% endhighlight %}

![Информационные кнопки на Foundation]({{site.url}}/images/uploads/2014/06/foundation_information_buttons.png)

### Другие варианты кнопок

Есть еще два класса для создания двух состояний кнопки. Первый класс `.disabled` делает кнопку неактивной с помощью CSS-свойства `cursor: default;`. Второй класс `.expand` заставляет кнопку занимать всю ширину блока-родителя и становиться просто огромной!

* `.disabled` - кнопка делается неактивной
* `.expand` - кнопка на всю ширину блока-родителя

HTML-код двух описанных выше кнопок:

{% highlight html %}
<a href="#" class="button disabled">disabled</a>
<a href="#" class="button expand">expand</a>
{% endhighlight %}

![Другие варианты кнопок на Foundation]({{site.url}}/images/uploads/2014/06/foundation_other_buttons.png)

### Тонкая настройка кнопок в Foundation

Помимо возможности использования готовых классов с предустановленными CSS-значениями, в фреймворке Foundation можно изменять значения по умолчанию из готового файла настроек. Данный файл называется `_settings.scss` и располагается в папке scss.

В этом файле собраны настройки в виде переменных Sass для всех компонентов фреймворка Foundation, но в данном случае нам необходимы переменные, отвечающие за настройку кнопок. Данные переменные находятся в секции файла, начинающейся со строки `BUTTONS`:

{% highlight css %}
$include-html-button-classes: $include-html-classes;

// Настройка величины padding кнопок
// $button-tny: rem-calc(10);
// $button-sml: rem-calc(14);
// $button-med: rem-calc(16);
// $button-lrg: rem-calc(18);

// Настройка блочной модели и нижнего margin кнопки
// $button-display: inline-block;
// $button-margin-bottom: rem-calc(20);

// Настройка шрифта надписей кнопок
// $button-font-family: $body-font-family;
// $button-font-color: #fff;
// $button-font-color-alt: #333;
// $button-font-tny: rem-calc(11);
// $button-font-sml: rem-calc(13);
// $button-font-med: rem-calc(16);
// $button-font-lrg: rem-calc(20);
// $button-font-weight: $font-weight-normal;
// $button-font-align: center;

// Настройка эффекта hover
// $button-function-factor: -20%;

// Настройка границ кнопок
// $button-border-width: 0px;
// $button-border-style: solid;
// $button-bg: $primary-color;
// $button-border-color: scale-color($bg, $lightness: $button-function-factor);

// Настройка радиуса скругления кнопок
// $button-radius: $global-radius;
// $button-round: $global-rounded;

// Настройка прозрачности кнопки с классом disabled
// $button-disabled-opacity: 0.7;
{% endhighlight %}

В принципе, элементарных знаний CSS должно быть достаточно, чтобы понять предназначение всех этих переменных. Поэтому давайте ради примера выполним пару изменений, чтобы увидеть результат. Для этого находим в файле `_settings.scss` строку `BUTTONS` (за поиск в Sublime Text отвечает сочетание клавиш Ctrl+F) и раскомментируем строки с теми переменными, которые нам необходимы.

Пусть это будут строки:

{% highlight css %}
$button-tny: rem-calc(10);
$button-font-color: #fff;
{% endhighlight %}

... в которых изменим значение переменных по умолчанию на:

{% highlight css %}
$button-tny: rem-calc(12);
$button-font-color: #ddd;
{% endhighlight %}

Если теперь заглянуть в инспектор свойств Firebug, то увидим, что padding для кнопки с классом `.tiny` увеличился; а также изменился цвет шрифта надписи с белого `#fff` на серый `#ddd`.

### Создание кнопок с помощью Sass

Рассмотренный выше способ редактирования значений переменных для тонкой настройки кнопок хорош. Но все-таки он утомителен и времязатратен - это нужно открыть файл `_settings.scss`, найти в нем Sass-переменные, раскомментировать их и изменить их значение.

Фреймворк Foundation имеет в своем арсенале еще один способ использования готовых CSS-классов и тонкой настройки Sass-переменных. Преимущество этого способа еще в том, что он по настоящему семантичен и позволяет не загромождать HTML-разметку чрезмерным количеством CSS-классов. Короче - этот способ использует Sass-миксины для подключения CSS-классов и изменения значений Sass-переменных.

Допустим, в нашей HTML-разметке имеется ссылка:

{% highlight html %}
<a class="readmore">Read More</a>
{% endhighlight %}

Чтобы превратить ее в кнопку на Foundation, нужно в файле `app.css` прописать следующее:

{% highlight css %}
.readmore{
  @include button;
}
{% endhighlight %}

В результате получим готовую кнопку! Чтобы иметь более тонкую настройку при создании кнопки, нужно передать миксину button переменные в качестве аргументов:

{% highlight css %}
.readmore{
  @include button($padding, $bg, $radius, $full-width, $disabled, $is-input);
}
{% endhighlight %}

Например, таким образом:

{% highlight css %}
.readmore{
  @include button($bg: #778899, $radius: true);
}
{% endhighlight %}

![Кнопка с помощью миксина на Foundation]({{site.url}}/images/uploads/2014/06/foundation_mixin_button.png)

На этом все.

---
