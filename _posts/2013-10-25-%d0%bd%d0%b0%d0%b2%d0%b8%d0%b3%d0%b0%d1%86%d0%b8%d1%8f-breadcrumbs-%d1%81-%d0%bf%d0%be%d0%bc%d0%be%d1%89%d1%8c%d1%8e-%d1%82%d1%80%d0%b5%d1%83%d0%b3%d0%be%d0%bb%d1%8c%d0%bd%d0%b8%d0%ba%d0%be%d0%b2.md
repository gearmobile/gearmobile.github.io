---
title: Навигация breadcrumbs с помощью треугольников на CSS
author: gearmobile
layout: post
permalink: /%d0%bd%d0%b0%d0%b2%d0%b8%d0%b3%d0%b0%d1%86%d0%b8%d1%8f-breadcrumbs-%d1%81-%d0%bf%d0%be%d0%bc%d0%be%d1%89%d1%8c%d1%8e-%d1%82%d1%80%d0%b5%d1%83%d0%b3%d0%be%d0%bb%d1%8c%d0%bd%d0%b8%d0%ba%d0%be%d0%b2/
ratings_users:
  - 6
ratings_score:
  - 16
ratings_average:
  - 2.67
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - breadcrumbs
---
Интересная статья по созданию навигации в виде &#8220;хлебных крошек&#8221; (breadcrumbs). Такая навигация удобна и полезна для сайтов с большим количеством рубрик. Благодаря такой навигации пользователь сайта может не запутаться в содержимом, точно знать, где он находиться и легко перейти в то место, куда ему нужно. Видов такой навигации может быть множество, все зависит от дизайна. Но принцип построения на CSS стандартный &#8211; с помощью списков ul.

Статья была опубликована на одном из моих любимых сайтов CSS-Tricks. Ниже привожу вольный перевод ее автора (Chris Coyier):

Вы уже знаете, как создавать треугольники на чистом CSS? Для этого просто генерируется блочный элемент с нулевой шириной и высотой, у которого имеется одна граница с цветом, а две смежные границы имеют прозрачный цвет. Такие треугольники применяются в самых разнообразных местах дизайна &#8211; например, для указателей в навигации. Другое место их применения &#8211; невинные украшательства дизайна, не нарушающие его общую разметку. В счастью, это возможно благодаря псевдо-элементам, которые часто используются при их создании. Применяя :before, :after или оба сразу можно сгенерировать блочные элементы и с их помощью создать треугольники. А вот последние можно применять для создания навигации в стиле &#8220;хлебные крошки&#8221;. Как выглядит одна из таких навигаций (чтобы иметь представление, что это такое), показано на рисунке ниже:<figure id="attachment_93" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/trianglebreadcrumbs-600x53.png" alt="Один из видов навигации хлебные крошки" width="600" height="53" class="size-medium wp-image-93" />][1]<figcaption class="wp-caption-text">Один из видов навигации хлебные крошки</figcaption></figure> 

### HTML разметка

Начнем создание такого меню с HTML-разметки, которая максимально проста и представляет собой обычный неупорядоченный список с классом breadcrumb:

<pre><ul class="breadcrumb">
  <li>
    <a href="#">Home</a>
  </li>
      
  
  <li>
    <a href="#">Vehicles</a>
  </li>
      
  
  <li>
    <a href="#">Vans</a>
  </li>
      
  
  <li>
    <a href="#">Camper Vans</a>
  </li>
      
  
  <li>
    <a href="#">1989 VW Westfalia Vanagon</a>
  </li>
    
</ul></pre>

### CSS код

В первую очередь убедимся, что наш список не выглядит, как обычный неупорядоченный список. Для этого уберем у него маркеры, сделаем его пункты плавающими влево и зададим самые общие стилевые правила для ссылок внутри этого списка. Обратите внимание на свойство overflow для всего списка в целом &#8211; он применяется здесь по двум причинам. Первая &#8211; наш список должен иметь высоту. Контейнеры, которые содержат только плавающие элементы, схлопываются (collapse), что совсем не то, что нам нужно. Второе &#8211; когда мы будем создавать треугольники, мы сделаем их достаточно большими:

<pre>.breadcrumb{
      list-style-type: none;
      overflow: hidden;
      font: 18px Helvetica, Arial, sans-serif;
    }
    .breadcrumb li{
      float: left;
    }
    .breadcrumb li a{
      float: left;
      position: relative;
      color: #fff;
      text-decoration: none;
      padding: 10px 0 10px 65px;
      background-color: brown;
      background-color: hsla(34, 85%, 35%, 1);
    }</pre>

Для создания треугольника мы воспользуемся псевдо-элементом :after. Для него установим высоту и ширину, равную нулю; и абсолютно спозиционируем его на 100% влево, что означает &#8211; он будет располагаться у правого края своего блока родителя. Затем сместим треугольник вниз на 50% и &#8220;вернем&#8221; назад на -50px для точного позиционирования по центру (это классический прием &#8211; перевод здесь). Есть только один момент, на который нужно обратить внимание. Граница, которую мы создаем сверху, равна 50px, нижняя граница также равна 50px, а ширина левой границы равна 30px. Это сделано для того, чтобы треугольник получился более &#8220;плоским&#8221;, с не такой острой вершиной. Если мы сделаем левую границу равной остальным сторонам в 50px, угол треугольника будет слишком острый. Так как верхняя и нижняя границы равны по 50px, то общая высота треугольника получается в 100px. Это гораздо больше, чем высота нашего меню, в котором высота шрифта 18px и padding-top: 10px, padding-bottom: 10px. Однако, это хорошо, что треугольник больше высоты меню. Это означает, что у нас остается достаточно свободного пространства, чтобы &#8220;поиграться&#8221; с размером шрифта:

<pre>.breadcrumb li a:after{
      content: '';
      display: block;
      position: absolute;
      top: 50%;
      margin-top: -50px;
      left: 100%;
      z-index: 2;
      width: 0;
      height: 0;
      border-left: 30px solid hsla(34, 85%, 35%, 1);
      border-top: 50px solid transparent;
      border-bottom: 50px solid transparent;
    }</pre>

Все хорошо. Но на примере, который нужно воссоздать в коде, есть тонкая полоска шириной в 1px, идущая по краю треугольника. Чтобы &#8220;нарисовать&#8221; ее в CSS-коде, нам потребуется еще &#8220;поколдовать&#8221;, так как напрямую создать границу для треугольника не получиться. Ведь треугольник как раз сам и является границей!

Поэтому мы поступим по другому &#8211; создадим еще один треугольник, который поместим позади нашего первого и зададим для него белый фоновый цвет. По своим свойствам второй треугольник будет практически одинаков с первым, но создаваться будет с помощью псевдо-элемента :before. Обратите внимание на важную вещь &#8211; z-index. С помощью этого свойства можно &#8220;тасовать&#8221; элементы :before и :after (точнее &#8211; созданные ими треугольники) в нужном порядке &#8211; какой треугольник над каким должен располагаться:

<pre>.breadcrumb li a:before{
      content: '';
      display: block;
      position: absolute;
      top: 50%;
      margin: -50px 0 0 1px;
      left: 100%;
      z-index: 1;
      width: 0;
      height: 0;
      border-left: 30px solid #fff;
      border-top: 50px solid transparent;
      border-bottom: 50px solid transparent;
    }</pre>

*Примечание переводчика:*

> Изменения минимальны. Цвет границы задан белым (#fff) и добавлено смещение треугольника влево на 1px (margin-left: 1px), чтобы разделительная черта была более заметна.

Теперь что касается цветовой заливки навигации. Так как пример имеет плавное изменение цвета элементов навигации, нам потребуются еще два замечательных CSS-свойства: nth-child и HSLa.

  * Чем полезно nth-child &#8211; можно задать цвета для различных элементов навигации без добавления дополнительной разметки в HTML-код;
  * Чем полезно HSLa &#8211; основываясь только на одном цвете, можно легко задать различные оттенки для элементов навигации.

Помимо этого, для первой ссылки мы уменьшим отступ слева с помощью padding-left, чтобы все элементы меню имели одинаковый размер; для последней ссылки совсем уберем цвет, сделаем некликабельной и вернем вид курсора по умолчанию. Все это мы выполним без какой-либо дополнительной разметки, с помощью псевдо-элементов :first-child и :last-child (плюс к двум предыдущим):

<pre>.breadcrumb li:first-child a {padding-left: 10px;}
    .breadcrumb li:nth-child(2) a {background-color: hsla(34,85%,45%,1);}
    .breadcrumb li:nth-child(2) a:after {border-left-color: hsla(34,85%,45%,1);}
    .breadcrumb li:nth-child(3) a {background-color: hsla(34,85%,55%,1);}
    .breadcrumb li:nth-child(3) a:after {border-left-color: hsla(34,85%,55%,1);}
    .breadcrumb li:nth-child(4) a {background-color: hsla(34,85%,65%,1);}
    .breadcrumb li:nth-child(4) a:after {border-left-color: hsla(34,85%,65%,1);}
    .breadcrumb li:nth-child(5) a {background-color: hsla(34,85%,75%,1);}
    .breadcrumb li:nth-child(5) a:after {border-left-color: hsla(34,85%,75%,1);}
    .breadcrumb li:last-child {background-color: transparent !important; color: #000; pointer-events: none; cursor: default;}</pre>

*Примечание переводчика:*

> Нумерация в nth-child начинается с единицы, а не с нуля, как принято в языках программирования.

И наконец, состояния элементов навигации при наведении курсора мыши. Здесь единственная особенность &#8211; нам нужно задать цвет треугольника точно таким же, как и ссылка. Не проблема:

<pre>.breadcrumb li a:hover {background-color: hsla(34,85%,25%,1);}
    .breadcrumb li a:hover:after {border-left-color: hsla(34,85%,25%,1) !important;}</pre>

### Совместимость с браузерами

Назовите меня ленивым, но я не занимался вопросом проверки данного кода на кросс-браузерную совместимость. Я был слишком захвачен самой идеей создания меню &#8220;хлебные крошки&#8221; на чистом CSS, чтобы думать его практическом использовании. Но если вас волнует мысль о его поддержке более старыми версиями браузеров, то стоит обратить внимание на следующие вещи:

  * используйте для передачи цвета HEX-код вместо HSLa;
  * для каждого из пунктов меню li создайте свои классы, вместо использования nth-child;
  * для браузеров, не поддерживающих псевдо-классы :after/:before используйте схему создания навигационного меню, основанную на изображениях;
  * применяйте библиотеку Modernizr для определения поддержки браузерами тех или иных свойств (например, HSLa);
  * используйте дополнительные стилевые правила для IE.

Результат, созданный с помощью приведенного выше кода, показан ниже:<figure id="attachment_95" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/breadcrumb-result-600x129.jpg" alt="Меню хлебные крошки с помощью CSS-треугольников" width="600" height="129" class="size-medium wp-image-95" />][2]<figcaption class="wp-caption-text">Меню хлебные крошки с помощью CSS-треугольников</figcaption></figure> 

Эффект при наведении курсора мыши на один из пунктов меню:<figure id="attachment_96" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/breadcrumb-result-hover-600x129.jpg" alt="Эффект при наведении курсора мыши на меню навигации" width="600" height="129" class="size-medium wp-image-96" />][3]<figcaption class="wp-caption-text">Эффект при наведении курсора мыши на меню навигации</figcaption></figure> 

На этом все и перевод закончен.

Оцените статью:  
<span id="post-ratings-91" class="post-ratings" data-nonce="84297fa0b6"><img id="rating_91_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(91, 1, '1 Star');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_91_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(91, 2, '2 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_91_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(91, 3, '3 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_91_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(91, 4, '4 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_91_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(91, 5, '5 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>6</strong> votes, average: <strong>2,67</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_91_text"></span></span><span id="post-ratings-91-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/10/trianglebreadcrumbs.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/10/breadcrumb-result.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/10/breadcrumb-result-hover.jpg