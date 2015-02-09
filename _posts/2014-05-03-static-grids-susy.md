---
title: Статические сетки с помощью Susy 2
author: gearmobile
layout: post
permalink: /static-grids-susy/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - susy
---
Иногда бываю ситуации, когда необходимо использовать сетки с фиксированной шириной, вместо обычного использования &#8220;резиновых&#8221; сеток. Плагин Susy 2 предоставляет возможность для работы с такими сетками. Но первоначально, необходимо выполнить несколько базовых настроек плагина для того, чтобы начать работать с такими сетками.<figure id="attachment_1168" style="width: 584px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/Susy.jpg" alt="Susy + Breakpoint" width="584" height="326" class="size-full wp-image-1168" />][1]<figcaption class="wp-caption-text">Susy + Breakpoint</figcaption></figure> 

Эта статья является третьей частью из серии руководства по плагину Susy 2. Если вы впервые познакомились с плагином Susy 2, то рекомендую начать его изучение с первой статьи &#8211; [Краткое руководство по Susy 2][2].

### Настройка Susy 2 для работы с фиксированной шириной

Для того, чтобы начать работать с фиксированной шириной элементов в плагине Susy 2, необходимо изменить значение одного из его параметров c `math: fluid` на `math: static`. Также необходимо задать ширину колонки через параметр `column-width`, для этого подойдут единицы измерения `px`, `em` или `rem`. В примере этой статьи будут использоваться пиксели (`px`).

Если планируется создавать адаптивную сетку, то значением параметра `column` необходимо установить число колонок при самом маленьком размере окна браузера.

Для начала создадим новый проект через Compass, указав на необходимость использования плагина Susy в нем:

<pre>compass create -r susy -u susy susy_static
</pre>

Затем откроем файл `_grids.scss` и добавим в него несколько следующих строк:

<pre>$susy: (
  math: static,
  columns: 4,
  column-width: 60px,
  gutters: 1/4,
  use-custom: (rem: true)
);
</pre>

### Создаем в Susy 2 статическую сетку

Шаги по созданию сетки с помощью плагина Susy 2 точно такие же, как если бы создавалась адаптивная сетка (*по умолчанию*). Первое, что необходимо сделать, это создать блок с классом `.container`. Однако, при этом не стоит забывать, что для статической сетки миксину `container` нужно передать аргумент в виде карты (*map*) через параметр `$susy`.

Когда плагин Susy 2 переключен в режим работы с фиксированной шириной сетки, ширина блока-обертки устанавливается в соотвествии с шириной колонки (`column-width`), число колонок (`columns`) и ширина gutter (`gutters`) также передаются в виде фиксированных величин. (Прим. переводчика: можно сказать немного по другому; все эти параметры с их значениями передаются миксину `container` через переменную `$susy`):

<pre>@import "grids";

.wrapper{
  @include container($susy);
}
</pre>

Плагин Susy 2 автоматически высчитает максимальную ширину сетки. Скомпилированный CSS-вид будет выглядет следующим образом:

<pre>.wrapper {
  width: 285px;
  margin-left: auto;
  margin-right: auto;
}
.wrapper:after {
  content: " ";
  display: block;
  clear: both;
}
</pre>

Единственное различие между статической и адаптивной сеткой заключается в том, в плагин Susy 2 расчитывает максимальную ширину блока-контейнера, в то время как в адаптивной сетке максимальная ширина всегда принимается равной 100%.

### Преобразование статической сетки в адаптивную в Susy 2

Создание адаптивной сетки с помощью плагина Susy 2 в режиме статической сетки практически ничем не отличается от того, как это можно делать в адаптивном режиме. За исключением того, что &#8230; вы уже догадались, это блок-обертка. В данной статье я затрону только изменение самого блока-контейнера. Если необходима более подробная информация об остальных моментах, вернитесь назад, к статье [Краткое введение в Susy 2 (Часть 2)][3].

При создании адаптивной сетки ее ширина всегда равна 100%. Поэтому нет необходимости явно ее задавать. Но в данном случае мы все-таки это сделаем.

К счастью, проблем с этим в плагине Susy 2 нет. Ниже показан наилучший метод, который можно только представить.

<pre>.wrapper{
    @include breakpoint(600px){
    @include container(12)
  }
}

.wrapper{
    @include breakpoint(900px){
    @include container(16)
  }
}
</pre>

В каждой из двух контрольных точек производится переопределение ширины блока-обертки путем задания числа колонок, которые будут входить с состав этого блока.

Скомпилированный CSS-код будет таким:

<pre>@media (min-width: 900px) {
  .wrapper {
    width: 1185px;
    margin-left: auto;
    margin-right: auto;
  }
  .wrapper:after {
    content: " ";
    display: block;
    clear: both;
  }
}
</pre>

Все работает, но выглядит досаточно неприглядно. Имеются дополнительные `margin-left` и `margin-right`, а также `clearfix`; это происходит потому, что блок-обертка был переопределен.

На этом серия статей по Susy 2 завершена.

Оцените статью:  
<span id="post-ratings-1166" class="post-ratings" data-nonce="d1e7760ead"><img id="rating_1166_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1166, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1166_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1166, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1166_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1166, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1166_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1166, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1166_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1166, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1166_text"></span></span><span id="post-ratings-1166-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/05/Susy.jpg
 [2]: http://localhost:7788/third/?p=1148
 [3]: http://localhost:7788/third/?p=1158