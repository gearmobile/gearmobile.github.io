---
title: Краткое введение в Susy 2 (Часть 2)
author: gearmobile
layout: post
permalink: /brief-tutorial-susy-part2/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 5
ratings_score:
  - 25
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - breakpoint
  - susy
---
В предыдущей статье были рассмотрены краткие основы плагина Susy 2 и на примере создана с помощью Susy довольно сложная HTML-разметка. В этой статье будет углубленное изучение плагина Susy 2. Сегодня предстоит изучить вопрос, каким образом можно легко и быстро создавать RWD (Responsive Web Design) с помощью Susy 2.

Если вы начали читать эту статью, но представления не имеете, что такое Susy 2 вообще, то вам стоит обратиться к предыдущей статье [Краткое руководство по Susy 2][1] &#8211; это стоит затраченного времени!

### Контрольные точки (breakpoints)

По умолчанию, плагин Susy 2 не имеет в своем составе миксина для создания контрольных точек (*breakpoints*). Наоборот, разработчики рекомендуют установить отдельно плагин [Breakpoint][2] и использовать его для создания медиа-запросов (*media-queries*).

Поэтому сначала произведем установку и импортирование этого плагина. *Прим. переводчика &#8211; имеется отдельная статья по установке и работе с плагином Breakpoint в Sass, расположенная по этому адресу &#8211; [Медиа-запросы Breakpoint в Sass][3].*

Плагин Breakpoint требует для своей работы наличия библиотеки Compass. Поэтому, сначала необходимо выполнить две команды по установке Compass и затем Breakpoint:

<pre>sudo gem install compass
sudo gem install breakpoint
</pre>

*Прим. переводчика: непонятно, что автор имел ввиду, но плагин Breakpoint для своей работы не нуждается в наличии библиотеки Compass. А вот препроцессор Sass ему необходим однозначно.*

Затем необходимо подключить плагин Breakpoint в конфигурационном файле `config.rb` и в файле `style.scss`:

<pre>// config.rb
# Require any additional compass plugins here.
require 'susy'
require 'breakpoint'
</pre>

<pre>// style.scss
@import "compass/reset";
@import "susy";
@import "breakpoint";
</pre>

Теперь все готово для того, чтобы двигаться дальше.

### Работаем с плагином Breakpoint

Если сказать одним предложением, что мне нравиться в использовании плагина Breakpoint, то это **легкость, с которой можно создавать контрольные точки в веб-дизайнах под мобильные устройства**. Давайте посмотрим, как это делается.

Для того, чтобы воспользоваться плагином Breakpoint, необходимо вызвать одноименный миксин и вставить его в код, передав требуемые аргументы. Эти аргументы преобразуются плагином Breakpoint в соответствующие медиа-запросы. Общий синтаксис миксина таков:

<pre>@include breakpoint(&lt;args>){
  // content
}
</pre>

Прелесть плагина Breakpoint в том, что если вы передаете ему только один аргумент, то он автоматически преобразуется в mobile-first. Этот аргумент должен быть значением минимальной ширины (`min-width`) разрабатываемого вами сайта, его контрольной точкой:

<pre>.container{
  @include breakpoint(1200px){
    // content
  }
}
</pre>

&#8230; что при компиляции в CSS-код даст результат:

<pre>@media (min-width: 1200px){
  .container{
    // content
  }
}
</pre>

Миксин Breakpoint очень гибкий и с помощью него при необходимости можно создавать [сложные медиа-запросы][4].

### Использование Breakpoint совместно с Susy 2

Предположим, необходимо создать CSS-сетку, которая будет меняться в определенной контрольной точке (*breakpoint*). Изначально все блоки CSS-сетки должны занимать всю ширину окна браузера в 900px. При превышении значения ширины окна в 900px CSS-сетка должна преобразовываться в 10-колоночный макет сайта, который был рассмотрен и создан в предыдущей статье. *Прим. переводчика &#8211; все в точности с принципом MobileFirst.*<figure id="attachment_1160" style="width: 573px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/susy_breakpoint_1-573x600.jpg" alt="Преобразование дизайна из Mobile View в Desktop View в Susy 2" width="573" height="600" class="size-medium wp-image-1160" />][5]<figcaption class="wp-caption-text">Преобразование дизайна из Mobile View в Desktop View в Susy 2</figcaption></figure> 

Для того, чтобы осуществить такую задачу, достаточно просто добавить нужную контрольную точку (*breakpoint*) в уже существующую таблицу стилей SCSS. В конкретном случае это будет выглядеть таким образом:

<pre>.column_1,.column_3{
  ...
  @include breakpoint(900px){
    @include span(2 of 10);
  }
}
.column_3{
  @include breakpoint(900px){
    @include last;
  }
}
...
.column_2{
  ...
  @include breakpoint(900px){
    @include span(6 of 10);
    @include clearfix;
    .column_2_1_1,.column_2_1_2{
      @include span(3 of 6);
    }
    .column_2_1_2{
      @include last;
    }
    .column_2_2_1{
      @include span(2 of 6);
    }
    .column_2_2_2{
      @include span(4 of 6 last);
      @include clearfix;
      .column_2_3_1,.column_2_3_2{
        @include span(2 of 4);
      }
      .column_2_3_2{
        @include last;
      }
      .column_2_4{
        @include span(full);
        clear: both;
      }
    }
  }
</pre>

То есть, для контрольной точки `min-width: 900px` создаются правила построения CSS-сетки с использованием плагина Susy 2. Если ширина окна браузера будет меньше 900px, все блоки будут располагаться на всю ширину вертикально (*по умолчанию &#8211; ведь это и есть нормальный поток*). При ширине окна больше 900px подключиться плагин Susy 2 и преобразует CSS-шаблон в 10-колоночный вид для Desktop. Все сделано с учетом принципа MobileFirst.

Готовый пример переработанного кода можно посмотреть здесь &#8211; [Susy 2 + Breakpoint][6].

Все выглядит достаточно просто и работает нормально. Но что, если требуется решить чуть более сложную задачу?

*Примечание автора: Если вам не нравиться использовать контрольные точки с помощью плагина Breakpoint, вы можете свободно применять старые добрые медиа-запросы (*media queries*), как это делается в CSS.*

### Добавляем несколько контрольных точек в Susy 2

Допустим, стоит задача создать еще одно состояние шаблона, промежуточное между состоянием Mobile View и состоянием Desktop View. Необходимо, чтобы при переходе от мобильного экрана к экрану монитора появилось еще одно состояние для планшетных компьютеров (Tablet View), с отдельной информационной колонкой справа:<figure id="attachment_1161" style="width: 389px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/susy_breakpoint_2-389x600.jpg" alt="Промежуточный дизайн Tablet View для планшетных компьютеров" width="389" height="600" class="size-medium wp-image-1161" />][7]<figcaption class="wp-caption-text">Промежуточный дизайн Tablet View для планшетных компьютеров</figcaption></figure> 

Этот случай выглядит немного сложнее, чем предыдущий. Главным образом потому, что блок `column_1` меняет свое положение и **перемещается слева направо**. Каким же образом можно осущесвить подобный маневр? Здесь необходимо применить небольшую хитрость.

Немного проанализируем будущий шаблон Tablet View для планшетного дизайна. В нем блоки `column_1` и `column_3` будут занимать 2 колонки из общих 6 колонок; в тоже время как блок `column_2` будет занимать 4 колонки из 6. Кроме того, блок `column_1` будет располагаться над блоком `column_3`.

Вся хитрость заключается в миксине `last` (*прим. переводчика: логично предположить, если до этого момента внимательно изучался результирующий CSS-код работы плагина Susy 2. Вот и profit чтения исходных кодов страницы!*).

Давайте взглянем на готовый SCSS-код и сразу многое станет понятно:

<pre>/* Tablet View
----------------------------*/
.column_1,.column_3{
  @include breakpoint(600px){
    @include span(2 of 6 last);
  }
}
.column_2{
  @include breakpoint(600px){
    @include span(4 of 6);
    @include clearfix;
    .column_2_1_1,.column_2_1_2{
      @include span(3 of 6);
    }
    .column_2_1_2{
      @include last;
    }
    .column_2_2_1, .column_2_2_2, .column_2_4{
      @include span(full);
    }
    .column_2_2_2{
      @include clearfix;
      .column_2_3_1,.column_2_3_2{
        @include span(2 of 4);
      }
      .column_2_3_2{
        @include last;
      }
      .column_2_4{
        clear: both;
      }
    }
  }
}
</pre>

Обратите внимание, что для блоков `.column_1` и `.column_3` изменилась их ширина и добавился миксин `last`. Если взглянуть на скомпилированный CSS-код, то увидим, что для этих блоков задано &#8220;плавание&#8221; вправо и убран правый `margin`:

<pre>@media (min-width: 600px) {
  .container .column_1, .container .column_3 {
    width: 31.03448%;
    float: right;
    margin-right: 0;
  }
}
</pre>

В то же время, для блока `.column_2` изменилась только его ширина, а &#8220;плавание&#8221; осталось прежним &#8211; влево. Вот в этом и заключается маленький секрет изменения раскладки блоков в шаблоне:

<pre>@media (min-width: 600px) {
  .container .column_2 {
    width: 65.51724%;
    float: left;
    margin-right: 3.44828%;
    overflow: hidden;
    *zoom: 1;
  }
</pre>

В блоке `.column_2` также были произведены изменения ширины некоторых блоков с тем, чтобы шаблон в этом виде максимально соответсвовал своему предназначению &#8211; использованию на планшетных компьютерах. В частности, была увеличена ширина блоков `.column_2_2_1`, `.column_2_2_2`, `.column_2_4` для того, чтобы ими было удобно пользоваться на небольшом экране.

Полный код получившегося примера можно посмотреть здесь &#8211; [Susy 2 + Breakpoint = Mobile View + Tablet View + Desktop View][8].

### Миксин Susy-Breakpoint

Плагин Susy 2 имеет в своем составе дополнительный миксин `susy-breakpoint`. Цель создания и применения этого миксина &#8211; сокращенная форма записи кода контрольных точек в Sass, в точности следуя принципу этого препроцессора &#8211; DRY.

Чтобы быть более понятным, приведу ниже кусочек кода, написанный с помощью миксина `susy-breakpoint` и точно такой же кусочек кода, написаный без этого миксина, как это делалось ранее в этой статье:

<pre>// C использованием миксина susy-breakpoint
.column_1,.column_3{
  @include susy-breakpoint(600px,6){
    @include span(2 last);
  }
}

// Без использования миксина susy-breakpoint
.column_1,.column_3{
  @include breakpoint(600px){
    @include span(2 of 6 last);
  }
}
</pre>

Видим, что миксин `susy-breakpoint` действительно использует сокращенную запись, в которой первый аргумент &#8211; это значение `breakpoint` (*контрольной точки*), а второй аргумент &#8211; число колонок, на которое разбита ширина шаблона. Тогда в миксине `span` достаточно указать число колонок из общего числа (которое равно 6), которое должен занимать указанный элемент. И что он является последним (`last`) с своем ряду (как дополнение).

Приведем ниже измененый SCSS и CSS-код нашего разрабатываемого примера, с учетом использования миксина `susy-breakpoint`:

<pre>.column_1,.column_3{
    @include susy-breakpoint(600px,6){
      @include span(2 last);
    }
  }
  .column_2{
    @include susy-breakpoint(600px,6){
      @include span(4);
      @include clearfix;
      ...
</pre>

<pre>@media (min-width: 600px) {
  .container .column_1, .container .column_3 {
    width: 31.03448%;
    float: right;
    margin-right: 0;
  }
}
@media (min-width: 600px) {
  .container .column_2 {
    width: 65.51724%;
    float: left;
    margin-right: 3.44828%;
    overflow: hidden;
    *zoom: 1;
  }
  ...
</pre>

Лично я предпочитаю использовать первый метод, с применением плагина Breakpoint (*прим. переводчика: мне он также кажется более наглядным и интуитивно понятным*). Естественно, можно с одинаковым успехом пользоваться обоими сопособами. Все зависит от того, какой вам больше нравиться и легче применять на практике.

В этом участке примеры вы, внимательный читатель, могли заметить, что допущена маленькая неточность, упущение. Связано оно с тем, что плавающему контейнеру разрешено занимать всю ширину окна браузера, даже если оно слишком большое. Давайте исправим этот недостаток.

### Ограничение блока-контейнера по ширине

Так как в этом примере используется плавающий контейнер, то ограничить его по ширине очень просто:

<pre>.container{
  @include container(1140px);
  ...
</pre>

В результате будет произведено ограничение блока с классом `.container` по максимальной ео ширине:

<pre>.container {
  background-color: #fbeecb;
  max-width: 1140px;
  ...
</pre>

Точно такого же результата можно добиться, если просто записать:

<pre>.container{
  background-color: #fbeecb;
  @include container;
  @include clearfix;
  max-width: 1140px;
  ...
</pre>

<pre>.container {
  background-color: #fbeecb;
  max-width: 1140px;
  ...
</pre>

К сожалению, точно также нельзя поступить в случае с CSS-сетками фиксированной ширины (*static grid*), потому что плагин Susy 2 производит все необходимые математические вычисления в CSS-сетке и расчет максимальной ширины блока-контейнера этой же CSS-сетки **одновременно**. Для построения CSS-сетки с фиксированной шириной необходим другой способ.

Но рассмотрение этого способа оставим на следующий раз, так как на сегодня уже достаточно.

Окончательный результат рассмотренного в этой статье шаблона можно посмотреть здесь &#8211; [Susy + Breakpoint = Final][9].

Данная статья является вольным переводом и обработкой оригинала &#8211; [A Complete Tutorial to Susy 2 (Part 2)][10].

Оцените статью:  
<span id="post-ratings-1158" class="post-ratings" data-nonce="a08ebd8469"><img id="rating_1158_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1158, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1158_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1158, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1158_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1158, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1158_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1158, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1158_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1158, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>5</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1158_text"></span></span><span id="post-ratings-1158-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1148
 [2]: http://breakpoint-sass.com/
 [3]: http://localhost:7788/third/?p=1065
 [4]: http://breakpoint-sass.com/#get_started
 [5]: http://localhost:7788/third/wp-content/uploads/2014/05/susy_breakpoint_1.jpg
 [6]: https://gist.github.com/roowa/11470192
 [7]: http://localhost:7788/third/wp-content/uploads/2014/05/susy_breakpoint_2.jpg
 [8]: https://gist.github.com/roowa/11472003
 [9]: https://gist.github.com/roowa/11473471
 [10]: http://www.zell-weekeat.com/susy2-tutorial-2/