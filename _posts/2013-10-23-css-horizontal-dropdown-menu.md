---
layout: post
title: "Создаем горизонтальное выпадающее меню на CSS"
author: gearmobile
tags: [css, dropdown menu]
---

В предыдущей статье "[Создаем вертикальное меню на CSS][1]" был освещен вопрос построения вертикального меню с подменю. В этой статье будет логическое продолжение этого вопроса и мы научимся делать горизонтальное меню с выпадающим подменю. Принцип построение и функционирования такой навигации очень похож на вертикальное меню, с той лишь разницей, что она будет располагаться горизонтально. В основе заложен тот же самый принцип - свойство `display` со значениями `none` и `block`.

При построении горизонтального меню нужно быть внимательным с принципом специфичности CSS, то есть - с вложенностью и каскадностью правил. Хорошим подспорьем в этом вопросе является SASS (SCSS), благодаря которому исключаются ошибки при соблюдении каскадности и наследовании свойств.

Код, написанный на SASS (SCSS) короче и логически читается проще, чем CSS. Поэтому, рекомендую изучить этот вопрос в статьях "[SASS (SCSS) в картинках - Часть 1][2]", "[SASS (SCSS) в картинках - Часть 2][3]".

Мы же приступим к созданию горизонтального меню с подменю "на коленках". Почему говорю так? Дело в том, что существует масса готовых примеров и кода, а также генераторов различных меню. Но они неинтересны - нам нужно разобраться в принципе построения и возможности самому написать такую навигацию. Как обычно, начинаем с каркаса меню, выполненного на HTML:

{% highlight html %}
<ul class="hormenu">
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
{% endhighlight %}

Структура подобного меню абсолютно одинакова со структурой вертикального меню. Также имеется внешний маркированный список с пунктами в виде ссылок, перед некоторыми из которых добавлены дополнительные подменю, выполненные также в виде маркированного списка. Различие между внешним и внутренним меню в классах, с помощью которых они будут видоизменяться. Помимо этого вы можете заметить, что у некоторых ссылок есть класс `arrow`, но о нем мы поговорим позже.

Приступим к оформлению нашего меню с помощью CSS. Сразу оговорюсь, что примеры кода, представленного здесь, написаны на SASS (SCSS). Начнем с того, что расположим навигацию горизонтально:

{% highlight css %}
.hormenu{
    margin: 50px 0 0 50px;
    overflow: hidden;
    li{
      float: left;
      margin-left: 1px;
      &:first-child{
        margin-left: 0;
      }
{% endhighlight %}

Думаю, ничего загадочного в этой части кода нет. Делаем отступ для меню и располагаем элементы `li` внутри него горизонтально с помощью свойства `float: left`. Предотвращаем схлопывание (`collapse`) блока-родителя `ul`, прописав для него `overflow: hidden`. Чтобы пункты меню были легко различимы, сделаем промежуток между ними с помощью левого `margin` в 1px. И для аккуратности уберем левый `margin` у первого элемента `li`.

Далее оформляем ссылки внутри пунктов `li`. Делаем ссылки блочными, чтобы кликабельной была вся область пункта навигации и задаем для нее высоту. Также указываем интерлиньяж, чтобы выровнять текст по вертикали и `text-align` для выравнивания по горизонтали. Цвет фона и цвет текста - как обычно.

Помимо этого, делаем ссылки с относительным позиционированием - оно нам пригодиться позже, когда будем отрисовывать треугольники. В этом коде стоит обратить внимание только на один момент - ширина элемента задается жестко. Это делается для того, чтобы основное меню не дергалось вправо-влево. Возможна ситуация, когда пункт подменю по ширине будет больше, чем пункт основного меню, и тогда ребенок "растянет" своего родителя.

При скрытии же подменю пункты основного меню будут "сжиматься", уменьшая ширину до своей собственной. Вот для этой цели и применяется явное задание ширины элемента `a`:

{% highlight css %}
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
{% endhighlight %}

Продолжим стилизацию нашей навигации и займемся подменю, а точнее - его подпунктами `li`. Уберем у этих элементов плавание влево `float` и левый `margin`, чтобы они не наследовали эти свойства. Убираем плавание, чтобы элементы `li` расположились вертикально, а левый `margin` - убрать "лесенку":

{% highlight css %}
li{
  float: none;
  margin: 0 0 1px 0;
{% endhighlight %}

Стилизуем ссылки пунктов подменю. Делаем фоновую заливку чуть светлее, чтобы отличалась от основного меню, а текст - чуть темнее по той же причине. Ну и анимация пунктов при наведении курсора мыши:

{% highlight css %}
a{
  background-color: #ccc + #111;
  color: #ccc - #333;
  &:hover{
    background-color: #ccc + #222;
  }
}
{% endhighlight %}

Теперь самое главное - сделаем подпункты меню выпадающими. Для этого сначала спрячем его, убрав из DOM-модели HTML-документа с помощью значения свойства `dislay: none`:

{% highlight css %}
.sub-hormenu{
  display: none;
{% endhighlight %}

&hellip; а затем будем показывать его только при наведении курсора мыши на пункт меню. Код здесь может показаться немного непонятным, но знак амперсанда означает тоже, что и класс `hormenu`:

{% highlight css %}
&:hover .sub-hormenu{
  display: block;
}
{% endhighlight %}

Все - наше меню создано и работает. Давайте немного приукрасив его, придав функциональности. А именно - на данный момент визуально невозможно различить, у какого пункта основного меню есть подменю, а у какого - нет. Для этого "продрисуем" к нужным пунктам небольшой треугольник с помощью псевдо-класса `:after`.

Как раз здесь нам и понадобиться относительное позиционирование для ссылок, о котором говорилось ранее. Создание стрелки "поручим" отдельному классу `arrow`, который будем "вешать" только на нужные нам ссылки:

{% highlight css %}
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
{% endhighlight %}

Вот, в принципе, и все. Основная задача выполнена и горизонтальное меню с выпадающим подменю у нас работает. Конечно, можно озадачиться целью "окрасить" активный пункт основного меню в тот же цвет, что и у подменю. Но эта проблема не входит в рассмотрение поставленной нами задачи. Ниже представлен полный код правил CSS (SCSS) для нашего меню:

{% highlight css %}
@import "compass/reset";

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
     &:first-child{
       margin-left: 0;
     }
     &:hover .sub-hormenu{
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
           &:hover{
             background-color: #ccc + #222;
           }
           &:after{
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
{% endhighlight %}

&hellip; и то, как оно выглядит:

<figure id="attachment_114" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu-600x254.jpg" alt="Горизонтальное меню на CSS" width="600" height="254" class="size-medium wp-image-114" />][4]
  <figcaption class="wp-caption-text">Горизонтальное меню на CSS</figcaption>
</figure>

<figure id="attachment_115" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu-with-dropdown-submenu-600x254.jpg" alt="Горизонтальное меню с выпадающим подменю" width="600" height="254" class="size-medium wp-image-115" />][5]
  <figcaption class="wp-caption-text">Горизонтальное меню с выпадающим подменю</figcaption>
</figure>

 [1]: http://localhost:7788/third/?p=109 "Создаем вертикальное меню на CSS"
 [2]: http://localhost:7788/third/?p=32 "SASS (SCSS) в картинках - Часть 1"
 [3]: http://localhost:7788/third/?p=44 "SASS (SCSS) в картинках - Часть 2"
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2013/11/css-horizontal-menu-with-dropdown-submenu.jpg
