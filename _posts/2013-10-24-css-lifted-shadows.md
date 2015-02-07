---
title: Создание приподнятых теней (lifted shadow) с помощью CSS
author: gearmobile
layout: post
permalink: /css-lifted-shadows/
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - lifted shadow
---
Создание приподнятых теней (lifted shadow) с помощью CSS. Такие тени создаются с помощью двух псевдо-элементов `:before` и `:after`. Дополнительной HTML-разметки при этом не требуется. Оба псевдо-элемента применяются только к одному элементу, который должен быть блочным. Ниже показана последовательность действий, которая совсем несложная. Статья написана по мотивам известного блога Николаса Галлахера, где показаны самые разнообразные виды таких сложных теней.

Приступаем к написанию кода. Создаем элемент `p` и для него прописываем правила (чтобы смотрелся хорошо):

**HTML:**

<pre><p class="lifted">
  Lifted Corners
</p></pre>

**CSS:**

<pre>.lifted{
  width: 400px;
  background-color: #fff;
  text-align: center;
  font-size: 18px;
  font-weight: bold;
  line-height: 70px;
  box-shadow: 0 0 40px rgba(0,0,0,0.3) inset;
  position: relative;
}
</pre>

Здесь все несложно. Задаем ширину и высоту блока, а также косметическую красоту типа выравнивания по центру и придания тени для блока. Не забываем сделать блок относительно позиционированным, так как в последующих шагах нам потребуются псевдо-элементы, которые нужно будет позиционировать относительно блока-родителя. Такой интересный момент в этом коде &#8211; нужно обязательно явно установить фоновый цвет для блока (`background-color: #fff`). Иначе он будет прозрачным по умолчанию и сквозь него будут проступать наши тени.

Необходимо получить две тени, одна из которых располагается под левым углом блока, а другая &#8211; под правым. Поэтому нам потребуются два псевдо-элемента &#8211; `:before` и `:after`. Создаем правила, общие для обоих псевдо-элементов:

<pre>.lifted:before, .lifted:after{
  content: '';
  position: absolute;
  width: 50%;
  height: 10%;
  bottom: 15px;
  left: 4px;
  z-index: -1;
  -webkit-box-shadow: 0 15px 10px rgba(0,0,0,0.6);
     -moz-box-shadow: 0 15px 10px rgba(0,0,0,0.6);
       -o-box-shadow: 0 15px 10px rgba(0,0,0,0.6);
          box-shadow: 0 15px 10px rgba(0,0,0,0.6);
}
</pre>

Немного &#8220;расшифруем&#8221; показанный выше код. Устанавливаем для обоих псевдо-элементов абсолютное позиционирование и координаты: от нижней границы 15px (`bottom: 15px`) и от левой границы 4px (`left: 4px;`). Ширину элемента устанавливаем в половину от ширины элемента-родителя (`width: 50%;`), высоту &#8211; 10% от ширины этого же элемента. Один интересный момент, про который не нужно забыть &#8211; &#8220;подсовываем&#8221; тени под блок-родитель с помощью свойства `z-index: -1`. Ну и создаем сами тени правилом `box-shadow: 0 15px 10px rgba(0,0,0,0.6)`, указав браузерные префиксы.

Теперь у нас есть обе тени, но выглядят они как одна, так как первая накладывается на другую, ибо их координаты одинаковы. Поэтому нужно &#8220;разнести&#8221; их по разным углам, установив для псевдо-элемента `:after` иное позиционирование по оси X:

<pre>.lifted:after{
  left: auto;
  right: 4px;
}
</pre>

Почти все готово. Осталось только сделать для обеих теней &#8220;косину&#8221;, то есть развернуть их на определенное количество градусов. Левую тень развернем против часовой стрелки, чтобы ее внутренний угол оказался под блоком-родителем. Правую развернем точно также, только по часовой стрелке, чтобы ее внутренний угол также &#8220;спрятался&#8221; под блоком. Разворачивание будем выполнять с помощью правила `transform: rotate` для псевдо-элемента `:before` -

<pre>-webkit-transform: rotate(-3deg);
   -moz-transform: rotate(-3deg);
     -o-transform: rotate(-3deg);
        transform: rotate(-3deg);
</pre>

и для псевдо-элемента `:after` -

<pre>-webkit-transform: rotate(3deg);
   -moz-transform: rotate(3deg);
     -o-transform: rotate(3deg);
        transform: rotate(3deg);
</pre>

Результат нашей работы можно посмотреть ниже. Красиво! <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" /><figure id="attachment_106" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/drop-down-shadows-600x281.jpg" alt="Блок с тенями под углами" width="600" height="281" class="size-medium wp-image-106" />][1]<figcaption class="wp-caption-text">Блок с тенями под углами</figcaption></figure> 

Можно немного усложнить задачу и сделать нижние уголки блока визуально приподнятыми. Создастся иллюзия того, что у блока завернутые вверх уголки, как у листочка бумаги. Для этого нужно вспомнить о том, что у свойства `border-radius` есть два параметра, а не одно. То есть, для одного угла можно задать два радиуса скругления, и тогда само скругление получиться не таким &#8220;правильным&#8221;, но более реалистичным. Первый радиус делаем большого размера, а второй немного меньше. В результате угол получается не скругленным, а немного скошенным. В нашем примере для блока-родителя задаем радиусы скругления нижних углов следующим образом:

<pre>border-bottom-left-radius: 40px 12px;
border-bottom-right-radius: 40px 12px;
</pre>

Итогом получается картинка листочка бумаги с завернутыми уголками:<figure id="attachment_107" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/curved-corners-600x281.jpg" alt="Завернутые уголки на чистом CSS" width="600" height="281" class="size-medium wp-image-107" />][2]<figcaption class="wp-caption-text">Завернутые уголки на чистом CSS</figcaption></figure> 

На сайте Николаса Галлахера есть множество других примеров создания теней, которые по-настоящему впечатляют. В этой статье приведен только один из них, самый распространенный. Как видите, ничего сложного в его создании нет. Но вот на кросс-браузерность такой пример мною не рассматривался, ибо мне был важен сам результат.

Оцените статью:  
<span id="post-ratings-105" class="post-ratings" data-nonce="3fa329032c"><img id="rating_105_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(105, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_105_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(105, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_105_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(105, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_105_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(105, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_105_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(105, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_105_text"></span></span><span id="post-ratings-105-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/drop-down-shadows.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/curved-corners.jpg