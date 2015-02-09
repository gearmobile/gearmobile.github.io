---
title: Создаем горизонтальное выпадающее меню на CSS
author: gearmobile
layout: post
permalink: /css-horizontal-dropdown-menu/
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - css
---
В предыдущей статье &#8220;[Создаем вертикальное меню на CSS][1]&#8221; был освещен вопрос построения вертикального меню с подменю. В этой статье будет логическое продолжение этого вопроса и мы научимся делать горизонтальное меню с выпадающим подменю. Принцип построение и функционирования такой навигации очень похож на вертикальное меню, с той лишь разницей, что она будет располагаться горизонтально. В основе заложен тот же самый принцип &#8211; свойство display со значениями `none` и `block`.

При построении горизонтального меню нужно быть внимательным с принципом специфичности CSS, то есть &#8211; с вложенностью и каскадностью правил. Хорошим подспорьем в этом вопросе является SASS (SCSS), благодаря которому исключаются ошибки при соблюдении каскадности и наследовании свойств. Код, написанный на SASS (SCSS) короче и логически читается проще, чем CSS. Поэтому, рекомендую изучить этот вопрос в статьях &#8220;[SASS (SCSS) в картинках &#8211; Часть 1][2]&#8220;, &#8220;[SASS (SCSS) в картинках &#8211; Часть 2][3]&#8220;.

Мы же приступим к созданию горизонтального меню с подменю &#8220;на коленках&#8221;. Почему говорю так? Дело в том, что существует масса готовых примеров и кода, а также генераторов различных меню. Но они неинтересны &#8211; нам нужно разобраться в принципе построения и возможности самому написать такую навигацию. Как обычно, начинаем с каркаса меню, выполненного на HTML:

<pre><ul class="hormenu">
  <li>
    <a class="arrow" href="#">Link_1</a>
          <ul class="sub-hormenu">
      <li>
        <a href="#">Link_1-1</a>
      </li>
              
      
      <li>
        <a href="#">Link_1-2</a>
      </li>
              
      
      <li>
        <a href="#">Link_1-3</a>
      </li>
              
      
      <li>
        <a href="#">Link_1-4</a>
      </li>
            
    </ul>
        
  </li>
      
  
  <li>
    <a href="#">Link_2</a>
  </li>
      
  
  <li>
    <a class="arrow" href="#">Link_3</a>
          <ul class="sub-hormenu">
      <li>
        <a href="#">Link_3-1</a>
      </li>
              
      
      <li>
        <a href="#">Link_3-2</a>
      </li>
              
      
      <li>
        <a href="#">Link_3-3</a>
      </li>
            
    </ul>
        
  </li>
      
  
  <li>
    <a href="#">Link_4</a>
  </li>
      
  
  <li>
    <a class="arrow" href="#">Link_5</a>
          <ul class="sub-hormenu">
      <li>
        <a href="#">Link_5-1</a>
      </li>
              
      
      <li>
        <a href="#">Link_5-2</a>
      </li>
              
      
      <li>
        <a href="#">Link_5-3</a>
      </li>
              
      
      <li>
        <a href="#">Link_5-4</a>
      </li>
              
      
      <li>
        <a href="#">Link_5-5</a>
      </li>
            
    </ul>
        
  </li>
    
</ul>
</pre>

Структура подобного меню абсолютно одинакова со структурой вертикального меню. Также имеется внешний маркированный список с пунктами в виде ссылок, перед некоторыми из которых добавлены дополнительные подменю, выполненные также в виде маркированного списка. Различие между внешним и внутренним меню в классах, с помощью которых они будут видоизменяться. Помимо этого вы можете заметить, что у некоторых ссылок есть класс `arrow`, но о нем мы поговорим позже.

Приступим к оформлению нашего меню с помощью CSS. Сразу оговорюсь, что примеры кода, представленного здесь, написаны на SASS (SCSS). Начнем с того, что расположим навигацию горизонтально:

<pre>.hormenu{
    margin: 50px 0 0 50px;
    overflow: hidden;
    li{
      float: left;
      margin-left: 1px;
      &#038;:first-child{
        margin-left: 0;
      }
</pre>

Думаю, ничего загадочного в этой части кода нет. Делаем отступ для меню и располагаем элементы li внутри него горизонтально с помощью свойства `float: left`. Предотвращаем схлопывание (collapse) блока-родителя ul, прописав для него `overflow: hidden`. Чтобы пункты меню были легко различимы, сделаем промежуток между ними с помощью левого `margin` в 1px. И для аккуратности уберем левый `margin` у первого элемента li.

Далее оформляем ссылки внутри пунктов li. делаем ссылки блочными, чтобы кликабельной была вся область пункта навигации и задаем для нее высоту. Также указываем интерлиньяж, чтобы выровнять текст по вертикали и `text-align` для выравнивания по горизонтали. Цвет фона и цвет текста &#8211; как обычно. Помимо этого, делаем ссылки с относительным позиционированием &#8211; оно нам пригодиться позже, когда будем отрисовывать треугольники. В этом коде стоит обратить внимание только на один момент &#8211; ширина элемента задается жестко. Это делается для того, чтобы основное меню не дергалось вправо-влево. Возможна ситуация, когда пункт подменю по ширине будет больше, чем пункт основного меню, и тогда ребенок &#8220;растянет&#8221; своего родителя. При скрытии же подменю пункты основного меню будут &#8220;сжиматься&#8221;, уменьшая ширину до своей собственной. Вот для этой цели и применяется явное задание ширины элемента `a`:

<pre>a{
    display: block;
    line-height: 25px;
    height: 25px;
    width: 130px;
    text-align: center;
    background-color: #ccc;
    color: #ccc - #555;
    position: relative;
  }
</pre>

Продолжим стилизацию нашей навигации и займемся подменю, а точнее &#8211; его подпунктами li. Уберем у этих элементов плавание влево (float) и левый `margin`, чтобы они не наследовали эти свойства. Убираем плавание, чтобы элементы li расположились вертикально, а левый `margin` &#8211; убрать &#8220;лесенку&#8221;:

<pre>li{
    float: none;
    margin: 0 0 1px 0;
</pre>

Стилизуем ссылки пунктов подменю. Делаем фоновую заливку чуть светлее, чтобы отличалась от основного меню, а текст &#8211; чуть темнее по той же причине. Ну и анимация пунктов при наведении курсора мыши:

<pre>a{
    background-color: #ccc + #111;
    color: #ccc - #333;
    &#038;:hover{
      background-color: #ccc + #222;
    }
  }
</pre>

Теперь самое главное &#8211; сделаем подпункты меню выпадающими. Для этого сначала спрячем его, убрав из DOM-модели HTML-документа с помощью значения свойства `dislay: none`:

<pre>.sub-hormenu{
    display: none;
</pre>

&#8230; а затем будем показывать его только при наведении курсора мыши на пункт меню. Код здесь может показаться немного непонятным, но знак амперсанда означает тоже, что и класс `hormenu`:

<pre>&#038;:hover .sub-hormenu{
    display: block;
  }
</pre>

Все &#8211; наше меню создано и работает. Давайте немного приукрасив его, придав функциональности. А именно &#8211; на данный момент визуально невозможно различить, у какого пункта основного меню есть подменю, а у какого &#8211; нет. Для этого &#8220;продрисуем&#8221; к нужным пунктам небольшой треугольник с помощью псевдо-класса `:after`. Как раз здесь нам и понадобиться относительное позиционирование для ссылок, о котором говорилось ранее. Создание стрелки &#8220;поручим&#8221; отдельному классу `arrow`, который будем &#8220;вешать&#8221; только на нужные нам ссылки:

<pre>.arrow:after{
    content: '';
    position: absolute;
    top: 50%;
    left: 80%;
    width: 0;
    height: 0;
    border-top: 4px solid #ccc - 666;
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
    margin-top: -2px;
  }
</pre>

Вот, в принципе, и все. Основная задача выполнена и горизонтальное меню с выпадающим подменю у нас работает. Конечно, можно озадачиться целью &#8220;окрасить&#8221; активный пункт основного меню в тот же цвет, что и у подменю. Но эта проблема не входит в рассмотрение поставленной нами задачи. Ниже представлен полный код правил CSS (SCSS) для нашего меню:

<pre>@import "compass/reset";

 a{
   text-decoration: none;
 }

 .arrow:after{
   content: '';
   position: absolute;
   top: 50%;
   left: 80%;
   width: 0;
   height: 0;
   border-top: 4px solid #ccc - 666;
   border-left: 4px solid transparent;
   border-right: 4px solid transparent;
   margin-top: -2px;
 }

 .hormenu{
   margin: 50px 0 0 50px;
   overflow: hidden;
   li{
     float: left;
     margin-left: 1px;
     &#038;:first-child{
       margin-left: 0;
     }
     &#038;:hover .sub-hormenu{
       display: block;
     }
     .sub-hormenu{
       display: none;
       li{
         float: none;
         margin: 0 0 1px 0;
         a{
           background-color: #ccc + #111;
           color: #ccc - #333;
           &#038;:hover{
             background-color: #ccc + #222;
           }
           &#038;:after{
             content: none;
           }
         }
       }
     }
     a{
       display: block;
       line-height: 25px;
       height: 25px;
       width: 130px;
       text-align: center;
       background-color: #ccc;
       color: #ccc - #555;
       position: relative;
     }
   }
 }
 
</pre>

&#8230; и то, как оно выглядит:<figure id="attachment_114" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu-600x254.jpg" alt="Горизонтальное меню на CSS" width="600" height="254" class="size-medium wp-image-114" />][4]<figcaption class="wp-caption-text">Горизонтальное меню на CSS</figcaption></figure> <figure id="attachment_115" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu-with-dropdown-submenu-600x254.jpg" alt="Горизонтальное меню с выпадающим подменю" width="600" height="254" class="size-medium wp-image-115" />][5]<figcaption class="wp-caption-text">Горизонтальное меню с выпадающим подменю</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-113" class="post-ratings" data-nonce="47ad1d9076"><img id="rating_113_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(113, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_113_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(113, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_113_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(113, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_113_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(113, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_113_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(113, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_113_text"></span></span><span id="post-ratings-113-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=109 "Создаем вертикальное меню на CSS"
 [2]: http://localhost:7788/third/?p=32 "SASS (SCSS) в картинках - Часть 1"
 [3]: http://localhost:7788/third/?p=44 "SASS (SCSS) в картинках - Часть 2"
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu-with-dropdown-submenu.jpg