---
title: Цикл for в Sass
author: gearmobile
excerpt: Очень краткий пример работы с циклом for в препроцессоре Sass. Создание и использование цикла for в препроцессоре Sass. Применение цикла for для задания цвета и кегля заголовков с первого (h1) по шестой (h6) уровень.
layout: post
permalink: /%d1%86%d0%b8%d0%ba%d0%bb-for-%d0%b2-sass/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 19
ratings_average:
  - 4.75
categories:
  - Статьи по CSS
tags:
  - sass
  - цикл for
---
Очень краткий пример работы с циклом `for` в препроцессоре Sass. С чего вдруг мне приспичило воспользоваться циклом в препроцессоре? Все, как всегда, просто &#8211; в предыдущей статье, посвященной плагину Smooth Scroll ([Плагин Smooth Scroll][1]), мне потребовался создать пример разметки HTML-документа с заголовками всех уровней, с первого (h1) до шестого (h6). Все бы ничего, но вручную создавать стили для заголовков всех уровней как-то **утомительно**.

### HTML-разметка для цикла for

Вот я и озаботился задачей автоматизировать этот процесс, через цикл. Для этой цели я использовал цикл `for`. Упростил пример, выкинув параграфы и оставив только заголовки всех уровней:

<pre><div class="wrapper">
  <h1>
    header 1
  </h1>
      
  
  <h2>
    header 2
  </h2>
      
  
  <h3>
    header 3
  </h3>
      
  
  <h4>
    header 4
  </h4>
      
  
  <h5>
    header 5
  </h5>
      
  
  <h6>
    header 6
  </h6>
    
</div>
  </pre>

### Базовые CSS-стили

Затем пропишу основные стили для этой разметки:

<pre>$color: #778899;
  $percent: 5%;
  $percentStep: 5;
  $fontSize: 76px;
  $fontSizeStep: 10;

  .wrapper{
    width: 60%;
    margin: 5% auto 0;
    text-align: center;
  }

  h1,h2,h3,h4,h5,h6{
    font-family: Arial, sans-serif;
    text-transform: capitalize;
    margin-bottom: 4%;
  }
  </pre>

### Использую цикл for в Sass

Теперь у меня стоит задача &#8220;покрасить&#8221; все заголовки в оттенки цвета, указанного в переменной `$color: #778899;`. Для создания оттенков воспользуюсь функцией `lighten()` из препроцессора Sass.

Цвет будет меняться с шагом в 5% (`$percentStep: 5;`):

<pre>h1{
    color: lighten($color,5%);
  }
  h2{
    color: lighten($color,10%);
  }
  h3{
    color: lighten($color,15%);
  }
  ...
  </pre>

Также будет изменяться размер шрифта (*кегль*) в заголовках уровней с первого (`h1`) до шестого (`h6`), с шагом 10px (`$fontSizeStep: 10`):

<pre>h1 {
    font-size: 76px;
  }
  h2 {
    font-size: 66px;
  }
  h3 {
    font-size: 56px;
  }
  ...
  </pre>

Как видим, задача и вправду не для ленивых &#8211; это же надо **тупо вбивать столько значений**! Но мне поможет Sass и его циклы, а точнее &#8211; цикл `for`.

Для этого создаю такую конструкцию цикла `for`:

<pre>@for $i from 1 through 6 {
    h#{$i}{
      color: lighten($color,$percent);
      font-size: $fontSize;
      $percent: $percent + $percentStep;
      $fontSize: $fontSize - $fontSizeStep;
    }
  }
  </pre>

Небольшая расшифровка приведенного выше цикла. В данном случае используется цикл `for`, в котором счетчик `$i` изменяет свое значение в диапазоне от 1 до 6 включительно. Конструкция `#{$i}` называется **экранированием** в Sass и служит для того, чтобы значение счетчика `$i` подставилось в коде &#8220;как есть&#8221;, в виде текста.

В результате получается такой вывод:

  * h1
  * h2
  * h3
  * h4
  * h5
  * h6

Далее идут CSS-правила с использованием функции `lighten()` препроцессора Sass и переменных `$color`, `$percent`, `$fontSize`. Последние две строки производят увеличение значения переменных на указанный шаг:

<pre>$percent: $percent + $percentStep;
  $fontSize: $fontSize - $fontSizeStep;
  </pre>

Приведенный выше SCSS-код скомпилируется в готовый CSS-код подобного вида:

<pre>h1 {
    color: #8695a4;
    font-size: 76px;
  }
  h2 {
    color: #94a2af;
    font-size: 66px;
  }
  h3 {
    color: #a3aeba;
    font-size: 56px;
  }
  h4 {
    color: #b1bbc5;
    font-size: 46px;
  }
  h5 {
    color: #c0c8d0;
    font-size: 36px;
  }
  h6 {
    color: #ced5db;
    font-size: 26px;
  }
  </pre>

Смотрим результат в браузере и радуемся успеху:<figure id="attachment_1540" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/sass_cycle-600x487.jpg" alt="Результат работы цикла for в Sass" width="600" height="487" class="size-medium wp-image-1540" />][2]<figcaption class="wp-caption-text">Результат работы цикла for в Sass</figcaption></figure> 

### Полный код примера цикла for в Sass

Полный код рассмотренного примера создания цикла `for` в Sass приведен ниже:

**HTML-код:**

<pre>
    

<div class="wrapper">
  <h1>
    header 1
  </h1>
        
  
  <h2>
    header 2
  </h2>
        
  
  <h3>
    header 3
  </h3>
        
  
  <h4>
    header 4
  </h4>
        
  
  <h5>
    header 5
  </h5>
        
  
  <h6>
    header 6
  </h6>
      
</div>
  
  </pre>

**SCSS-код:**

<pre>@import "compass/reset";

  $color: #778899;
  $percent: 5%;
  $percentStep: 5;
  $fontSize: 76px;
  $fontSizeStep: 10;

  .wrapper{
    width: 60%;
    margin: 5% auto 0;
    text-align: center;
  }

  h1,h2,h3,h4,h5,h6{
    font-family: Arial, sans-serif;
    text-transform: capitalize;
    margin-bottom: 4%;
  }

  @for $i from 1 through 6 {
    h#{$i}{
      color: lighten($color,$percent);
      font-size: $fontSize;
      $percent: $percent + $percentStep;
      $fontSize: $fontSize - $fontSizeStep;
    }
  }
  </pre>

Скомпилированный в **CSS-код** результат нашего кодинга:

<pre>.wrapper {
    width: 60%;
    margin: 5% auto 0;
    text-align: center;
  }

  h1, h2, h3, h4, h5, h6 {
    font-family: Arial, sans-serif;
    text-transform: capitalize;
    margin-bottom: 4%;
  }

  h1 {
    color: #8695a4;
    font-size: 76px;
  }

  h2 {
    color: #94a2af;
    font-size: 66px;
  }

  h3 {
    color: #a3aeba;
    font-size: 56px;
  }

  h4 {
    color: #b1bbc5;
    font-size: 46px;
  }

  h5 {
    color: #c0c8d0;
    font-size: 36px;
  }

  h6 {
    color: #ced5db;
    font-size: 26px;
  }
  </pre>

Оцените статью:  
<span id="post-ratings-1537" class="post-ratings" data-nonce="0fb507fc06"><img id="rating_1537_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1537, 1, '1 Star');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1537_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1537, 2, '2 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1537_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1537, 3, '3 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1537_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1537, 4, '4 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1537_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1537, 5, '5 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>4,75</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1537_text"></span></span><span id="post-ratings-1537-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1527 "Плагин Smooth Scroll"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/07/sass_cycle.jpg