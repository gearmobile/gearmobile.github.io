---
title: 'Знакомимся с &#8220;тихими&#8221; placeholder'
author: gearmobile
excerpt: Знакомство с селекторами placeholder в препроцессоре Sass. Что они из себя представляют и в чем преимущество директивы @extend перед директивой @include.
layout: post
permalink: /sass-selector-placeholder/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 16
ratings_average:
  - 4
categories:
  - Статьи по CSS
tags:
  - placeholder
  - sass
---
> Статья посвящена вопросу &#8220;тихих&#8221; placeholder&#8217;ов в препроцессоре Sass. Что это такое и в чем преимущество их использования. Оригинал статьи размещен здесь &#8211; [Understanding placeholder selectors][1].

Препроцессор Sass предоставляет несколько способов создания одного фрагмента кода, который будет многократно использоваться внутри CSS-кода.

Например, можно воспользоваться миксинами (`mixins`) для вставки группы CSS-свойств (или CSS-правил) в CSS-коде.

Или же использовать директиву `@extend` для расширения набора CSS-свойств одного HTML-элемента за счет CSS-свойств другого HTML-элемента.

В Sass версии 3.2 введена новая концепция под названием `placeholder`, которая делает использование директивы `@extend` еще более эффективным способом.

Но прежде чем мы перейдем к рассмотрению этого нововведенния, давайте остановимся на моменте, каким образом работает расширение (`@extend`) CSS-свойств в Sass.

### Как работает @extend

Директива `@extend` в препроцессоре Sass позволяет CSS-селекторам с легкостью **обмениваться** между собой своими CSS-свойствами. Лучше всего вышесказанное можно проиллюстрировать на живом примере:

<pre>// SCSS

  .icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    @extend .icon;
    /* здесь - специфичные стили класса .error-icon */
  }

  .info-icon {
    @extend .icon;
    /* здесь - специфичные стили класса .info-icon */
  }
</pre>

Результатом компиляции этого SCSS-кода в CSS-код будет следующий фрагмент:

<pre>// CSS

  .icon, .error-icon, .info-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    /* здесь - специфичные стили класса .error-icon */
  }

  .info-icon {
    /* здесь - специфичные стили класса .info-icon */
  }
</pre>

Рассмотрим &#8220;механизм&#8221; показанного выше примера более детально. В нем директива `@extend` играет ключевую роль. С помощью нее селекторы `.error-icon` и `.info-icon` **наследуют** свойства селектора `.icon`. При изменении CSS-свойств селектора `.icon` автоматически будут меняться свойства селекторов `.error-icon` и `.info-icon`, так как они наследуют определенный набор CSS-свойств у селектора `.icon`. Довольно изящный подход, не правда ли?

А вот теперь наступает интересный момент. Что, если элемент с классом `.icon` **не планируется использовать** и он даже **не будет присутствовать** в HTML-разметке? Но CSS-свойства этого элемента нам нужны для стилизации элементов `.error-icon` и `.info-icon`.

Получается, что результирующий CSS-код будет **неоправданно раздут** из-за того, что в нем присутствует &#8220;лишний&#8221; элемент, который напрямую никогда не будет использован.

И тут наступает момент для выхода на сцену героя этой статьи &#8211; **селектора placeholder** (его еще называют &#8220;тихим&#8221; placeholder&#8217;ом):<figure id="attachment_2045" style="width: 400px;" class="wp-caption aligncenter">

[<img class="wp-image-2045 size-full" src="http://localhost:7788/third/wp-content/uploads/2014/11/placeholder.jpg" alt="placeholder" width="400" height="300" />][2]<figcaption class="wp-caption-text">&#8220;Тихий&#8221; placeholder</figcaption></figure> 

### Знакомимся с селектором placeholder

Селекторы placeholder были введены в Sass как раз для того, чтобы решать вышеназванную проблему. Синтаксис placeholder очень похож на синтаксис обычных CSS-классов, только вместо точки (`.`) перед именем ставиться **символ процента** (`%`).

Селекторы placeholder имеют одну специфичную для них особенность &#8211; они никак не проявляют себя в скомпилированном CSS-коде. Можно сказать по другому &#8211; вы никогда не найдете селекторов placeholder в результирующем CSS-коде (поэтому они и носят такое название &#8211; &#8220;тихие&#8221; placeholder). В скомпилированном CSS-коде будут только селекторы, которые **используют** &#8220;тихие&#8221; placeholder&#8217;ы, но никак не сами &#8220;тихие&#8221; placeholder&#8217;ы.

Вернемся назад, к нашему начальному примеру. Заменим в нем имя класса `.icon` на имя &#8220;тихого&#8221; placeholder&#8217;а &#8211; `%icon`:

<pre>// SCSS

  %icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    @extend %icon;
    /* здесь - специфичные стили класса .error-icon */
  }

  .info-icon {
    @extend %icon;
    /* здесь - специфичные стили класса .info-icon */
  }
</pre>

В результате скомпилированный CSS-код будет выглядеть таким образом:

<pre>// CSS

  .error-icon, .info-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    /* здесь - специфичные стили класса .error-icon */
  }

  .info-icon {
    /* здесь - специфичные стили класса .info-icon */
  }
</pre>

Обратите внимание на важный момент &#8211; класс `.icon` теперь **не присутствует** в результирующем CSS-коде! Его там нет!

### @extend или @include

На первый взгляд может показаться, что &#8220;тихие&#8221; placeholder &#8211; это почти тоже самое, что и миксины (`mixin`). С функциональной точки зрения такое утверждение абсолютно верно &#8211; результат в браузере получается идентичным. А вот с точки зрения CSS разница **очень существенная**!

Давайте снова изменим наш первоначальный пример и теперь воспользуемся миксином `@mixin icon`:

<pre>// SCSS

  @mixin icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  .error-icon {
    @include icon;
    /* здесь - специфичные стили класса .error-icon */
  }

  .info-icon {
    @include icon;
    /* здесь - специфичные стили класса .info-icon */
  }
</pre>

Посмотрим на сгенерированный CSS-код:

<pre>// CSS

  .error-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
    /* здесь - специфичные стили класса .error-icon */
  }

  .info-icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
    /* здесь - специфичные стили класса .info-icon */
  }
</pre>

С точки зрения разработки данный пример ничем не хуже примера с использованием &#8220;тихого&#8221; placeholder&#8217;а.

Но обратите внимание на тот факт, что CSS-правила `transition: background-color ease .2s;` и `margin: 0 .5em;` **дублируются** между селекторами `.error-icon` и `.info-icon`, что приводит к **неоправданному раздутию кода**. В случае использования &#8220;тихого&#8221; placeholder **этого не происходит**.

### Ограничения

Использование директивы `@extend` имеет одно ограничение, связанное с тем, что применение &#8220;тихих&#8221; placeholder&#8217;ов никак **не оправдывает себя в медиа-запросах** `@media`.

Рассмотрим такой пример:

<pre>// SCSS

  %icon {
    transition: background-color ease .2s;
    margin: 0 .5em;
  }

  @media screen {

    .error-icon {
      @extend %icon;
    }

    .info-icon {
      @extend %icon;
    }

  }
</pre>

Видим, что в данном случае &#8220;тихий&#8221; placeholder добавлен для селекторов, находящихся внутри медиа-запроса `@media`.

Однако, при попытке компиляции этого SCSS-кода в CSS-код получиться ошибка:

> You may not @extend an outer selector from within @media. You may only @extend selectors within the same directive. From &#8220;@extend %icon&#8221; on line 8 of icons.scss

Когда я первый раз увидел такую ошибку, то подумал, что это баг. Но по зрелом размышлении пришел к выводу, что в данном подходе все правильно.

Механизм работы директивы `@extend` основан на **добавлении одного селектора к другому селектору** без необходимости дублировать CSS-свойства этих селекторов. Однако невозможно объединять селекторы, находящиеся в разных медиа-запросах `@media`.

Но можно поступить по другому, чтобы выйти из данной затруднительной ситуации. Любой медиа-запрос, который служит оберткой для &#8220;тихого&#8221; placeholder, распространяют свои свойства на селекторы, не размещенные внутри этого запроса. Выражение достаточно запутанное, поэтому лучше приведу пример:

<pre>// SCSS

  @media screen {
    %icon {
      transition: background-color ease .2s;
      margin: 0 .5em;
    }
  }

  .error-icon {
    @extend %icon;
  }

  .info-icon {
    @extend %icon;
  }
</pre>

Компиляция пройдет без ошибок и ее результатом будет CSS-код:

<pre>// CSS

  @media screen {
    .error-icon, .info-icon {
      transition: background-color ease .2s;
      margin: 0 .5em;
    }
  }
</pre>

### Заключение

Обе директивы `@extend` и `@include` являются очень полезными инструментами, между которыми существует тонкое различие. Если вопрос производительности генерируемого CSS-кода имеет для вас важное значение или же перед вами стоит проблема повторяемости кода, то решением будет являться директива `@extend`. В некоторых случая `@extend` значительно упрощает получаемый CSS-код и улучшает его производительность.

Конечно же, ничто не мешает вам смешивать между собой директиву `@extend` и миксин `mixin` (*если этого требуют обстоятельства*):

<pre>// SCSS

  @media screen {
    %icon {
      transition: background-color ease .2s;
      margin: 0 .5em;
    }
  }

  @mixin icon($color, $url) {
    @extend %icon;
    background-color: $color;
    background-url: url($url);
  }

  .error-icon {
    @include icon(red, '/images/error.png');
  }

  .info-icon {
    @include icon(blue, '/images/info.png');
  }
</pre>

Однако, в разработке я придерживаюсь такого подхода, когда исходный код легко читается и поддерживается.

Оцените статью:  
<span id="post-ratings-2044" class="post-ratings" data-nonce="8e6bdfcbef"><img id="rating_2044_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2044, 1, '1 Star');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2044_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2044, 2, '2 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2044_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2044, 3, '3 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2044_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2044, 4, '4 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2044_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2044, 5, '5 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>4,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2044_text"></span></span><span id="post-ratings-2044-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://thesassway.com/intermediate/understanding-placeholder-selectors "Understanding placeholder selectors"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/11/placeholder.jpg