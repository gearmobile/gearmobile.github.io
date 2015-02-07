---
title: 'Foundation &#8211; создаем кнопки'
author: gearmobile
excerpt: Продолжение обзора фреймворка Foundation, в котором приступим к практической части и научимся создавать кнопки на этом фреймворке. Почему сразу такой быстрый переход r практике? Я сам всегда так учился всему учился и считаю, что это наилучший способ научиться что-либо делать. Нежели долго и нудно жевать сопли теории, чтобы когда-нибудь перейти к практике. Остальные основы Foundation я буду изучать с вами в дальнейшем, шаг за шагом.
layout: post
permalink: /foundation-create-buttons/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 20
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - foundation
---
Продолжение обзора фреймворка Foundation, в котором приступим к практической части и научимся создавать кнопки на этом фреймворке. Почему сразу такой быстрый переход к практике? Я сам всегда так учился всему и считаю, что это наилучший способ научиться что-либо делать. Нежели долго и нудно жевать сопли теории, чтобы когда-нибудь перейти к практике. Остальные основы Foundation я буду изучать с вами в дальнейшем, шаг за шагом.

Итак, в [первой части знакомства с Foundation][1] я с вами установил фреймворк Foundation c поддержкой Sass/Compass под операционной системой Linux Mint 17 и подготовил его к работе. Давайте откроем созданный утилитой foundation индексный файл index.html и рассмотрим его содержимое. &#8220;Шапка&#8221; head этого HTML-документа не представляет из себя что-то особенное, кроме двух строк:

<pre><link rel="stylesheet" href="css/app.css" />
</pre>

В первой строке производится подключение файла CSS-стилей `app.css`, который служит для создания пользовательских CSS-правил. Другими словами, фреймворк Foundation представляет из себя набор готовых CSS-стилей (на то он и фреймворк). Но не всегда готовые CSS-стили отвечают конкретным требованиям дизайна страницы. Чтобы изменить или переопределить готовые CSS-стили фреймворка Foundation, служит таблица стилей `app.css` &#8211; именно туда нужно вносить свои собственные CSS-правила.

Вторая строка &#8211; это подключение библиотеки Modernizr и больше тут сказать нечего.

Если заглянуть в самый конец HTML-документа, то увидим три строки подключения js-скриптов перед закрывающим тегом `</body>`:

<pre></pre>

Ситуация здесь почти такая же, как и с &#8220;шапкой&#8221; head документа. Подключается библиотека jQuery (куда же без нее?), коллекция готовых js-скриптов от Foundation `foundation.min.js` для создания разнообразных меню, табов и тому подобное. Скрипт `app.js` служит для тех же целей, что и таблица стилей `app.css` &#8211; для внесения пользовательских изменений.

Между тегами `<body></body>` размещено содержимое документа в виде CSS-сетки Grid, к которой я вернусь немного позже. Сейчас я произвожу очистку этого содержимого, чтобы писать в нем свой собственный HTML-код.

### Кнопки на Foundation

Создание кнопок на фреймворке Foundation **занятие малоутомительное**. Для этой цели используется тег `a`, которому присваивается имя готового CSS-класса `.button`. Помимо этого, имеются три или четыре группы классов, с помощью которых можно создавать различные варианты кнопок &#8211; разного цвета, формы и назначения.

Кнопки, созданные на Foundation c помощью предопределенных классов, имеют полностью готовый вид, вплоть до CSS-свойства transition.

#### Обычная кнопка на Foundation

Как я уже упоминал выше, для создания кнопки под Foundation достаточно присвоить тегу `a` имя готового класса `.button`. Давайте так и сделаем:

<pre><a href="#" class="button">read more</a>
  </pre><figure id="attachment_1403" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_simple_button-600x169.png" alt="Обычная кнопка на Foundation" width="600" height="169" class="size-medium wp-image-1403" />][2]<figcaption class="wp-caption-text">Обычная кнопка на Foundation</figcaption></figure> 

Все очень просто. Готовый результат можно посмотреть в браузере. Я же перейду к более интересному вопросу создания различных модификаций (вариантов) стандартной кнопки `.button`.

#### Кнопки разных размеров

Начнем с группы классов, служащих для создания **кнопок различных размеров**. В этой группе имеются четыре класса для создания **четырех размеров кнопок**:

  * .tiny &#8211; крошечная кнопка
  * .small &#8211; маленькая кнопка
  * .medium &#8211; средняя кнопка
  * .large &#8211; большая кнопка

В качестве примера приведу ниже HTML-код создания таких кнопок:

<pre><a href="#" class="button tiny">tiny</a>
  <a href="#" class="button small">small</a>
  <a href="#" class="button medium">medium</a>
  <a href="#" class="button large">large</a>
  </pre><figure id="attachment_1404" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_sizes_of_buttons-600x200.png" alt="Кнопки разных размеров на Foundation" width="600" height="200" class="size-medium wp-image-1404" />][3]<figcaption class="wp-caption-text">Кнопки разных размеров на Foundation</figcaption></figure> 

Как видно из приведенного выше кода, используется мультиклассовость &#8211; добавление к классу `.button` любого из классов размера кнопки &#8211; `.tiny`, `.small`, `.medium`, `.large`. Смешение CSS-правил обоих классов дает в результате нужный вид кнопки. Впрочем, все это должно быть известно из основ CSS.

#### Скругленные кнопки на Foundation

В фреймворке имеются два готовых класса для создания скругленной формы у кнопки. Первый класс &#8211; `.radius` задает радиус скругления углов у кнопки. Второй радиус `.round` создает круглую кнопку.

  * `.radius` &#8211; радиус ускругления углов у кнопки
  * `.round` &#8211; круглая кнопка

HTML-код создания таких кнопок показан ниже:

<pre><a href="#" class="button radius">radius</a>
  <a href="#" class="button round">round</a>
  </pre><figure id="attachment_1405" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_rounded_buttons-600x131.png" alt="Скругленные кнопки на Foundation" width="600" height="131" class="size-medium wp-image-1405" />][4]<figcaption class="wp-caption-text">Скругленные кнопки на Foundation</figcaption></figure> 

#### Информационные кнопки на Foundation

Не знаю, точно ли такое название отражает предназначение подобных кнопок, но на другом фреймворке &#8211; Twitter Bootstrap как имеется такое название для этих кнопок, поэтому решил и в Foundation назвать их также.

  * `.secondary` &#8211; обычная кнопка
  * `.success` &#8211; кнопка, информирующая об успешном выполнении задачи
  * `.alert` &#8211; кнопка предупреждения о чем-либо

HTML-код для создания информационных кнопок:

<pre><a href="#" class="button secondary">secondary</a>
  <a href="#" class="button success">success</a>
  <a href="#" class="button alert">alert</a>
  </pre><figure id="attachment_1406" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_information_buttons-600x177.png" alt="Информационные кнопки на Foundation" width="600" height="177" class="size-medium wp-image-1406" />][5]<figcaption class="wp-caption-text">Информационные кнопки на Foundation</figcaption></figure> 

#### Другие варианты кнопок

Есть еще два класса для создания двух состояний кнопки. Первый класс `.disabled` делает кнопку неактивной с помощью CSS-свойства `cursor: default;`. Второй класс `.expand` заставляет кнопку занимать всю ширину блока-родителя и становиться просто огромной!

  * `.disabled` &#8211; кнопка делается неактивной
  * `.expand` &#8211; кнопка на всю ширину блока-родителя

HTML-код двух описанных выше кнопок:

<pre><a href="#" class="button disabled">disabled</a>
  <a href="#" class="button expand">expand</a>
  </pre><figure id="attachment_1407" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_other_buttons-600x128.png" alt="Другие варианты кнопок на Foundation" width="600" height="128" class="size-medium wp-image-1407" />][6]<figcaption class="wp-caption-text">Другие варианты кнопок на Foundation</figcaption></figure> 

#### Тонкая настройка кнопок в Foundation

Помимо возможности использования готовых классов с предустановленными CSS-значениями, в фреймворке Foundation можно изменять значения по умолчанию из готового файла настроек. Данный файл называется `_settings.scss` и располагается в папке scss. В этом файле собраны настройки в виде переменных Sass для всех компонентов фреймворка Foundation, но в данном случае нам необходимы переменные, отвечающие за настройку кнопок. Данные переменные находятся в секции файла, начинающейся со строки `BUTTONS`:

<pre>$include-html-button-classes: $include-html-classes;

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
  </pre>

В принципе, элементарных знаний CSS должно быть достаточно, чтобы понять предназначение всех этих переменных. Поэтому давайте ради примера выполним пару изменений, чтобы увидеть результат. Для этого находим в файле `_settings.scss` строку `BUTTONS` (за поиск в Sublime Text отвечает сочетание клавиш Ctrl+F) и раскомментируем строки с теми переменными, которые нам необходимы.

Пусть это будут строки:

<pre>$button-tny: rem-calc(10);
  $button-font-color: #fff;
  </pre>

&#8230; в которых изменим значение переменных по умолчанию на:

<pre>$button-tny: rem-calc(12);
  $button-font-color: #ddd;
  </pre>

Если теперь заглянуть в инспектор свойств Firebug, то увидим, что padding для кнопки с классом `.tiny` увеличился; а также изменился цвет шрифта надписи с белого `#fff` на серый `#ddd`.

#### Создание кнопок с помощью Sass

Рассмотренный выше способ редактирования значений переменных для тонкой настройки кнопок хорош. Но все-таки он утомителен и времязатратен &#8211; это нужно открыть файл `_settings.scss`, найти в нем Sass-переменные, раскомментировать их и изменить их значение.

Фреймворк Foundation имеет в своем арсенале еще один способ использования готовых CSS-классов и тонкой настройки Sass-переменных. Преимущество этого способа еще в том, что он по настоящему семантичен и позволяет не загромождать HTML-разметку чрезмерным количеством CSS-классов. Короче &#8211; этот способ использует Sass-миксины для подключения CSS-классов и изменения значений Sass-переменных.

Допустим, в нашей HTML-разметке имеется ссылка:

<pre><a class="readmore">Read More</a>
  </pre>

Чтобы превратить ее в кнопку на Foundation, нужно в файле `app.css` прописать следующее:

<pre>.readmore{
    @include button;
  }
  </pre>

В результате получим готовую кнопку! Чтобы иметь более тонкую настройку при создании кнопки, нужно передать миксину button переменные в качестве аргументов:

<pre>.readmore{
    @include button($padding, $bg, $radius, $full-width, $disabled, $is-input);
  }
  </pre>

Например, таким образом:

<pre>.readmore{
    @include button($bg: #778899, $radius: true);
  }
  </pre><figure id="attachment_1408" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_mixin_button-600x64.png" alt="Кнопка с помощью миксина на Foundation" width="600" height="64" class="size-medium wp-image-1408" />][7]<figcaption class="wp-caption-text">Кнопка с помощью миксина на Foundation</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-1399" class="post-ratings" data-nonce="a42dc6fe0c"><img id="rating_1399_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1399, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1399_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1399, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1399_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1399, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1399_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1399, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1399_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1399, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1399_text"></span></span><span id="post-ratings-1399-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1386 "Фреймворк Foundation - Знакомство"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_simple_button.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_sizes_of_buttons.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_rounded_buttons.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_information_buttons.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_other_buttons.png
 [7]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_mixin_button.png