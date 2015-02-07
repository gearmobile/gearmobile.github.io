---
title: Библиотека Animate.css
author: gearmobile
excerpt: Библиотека Animate.css предназначена для создания красивых CSS3-эффектов на HTML-странице. Подключение библиотеки и ее использование возможно с помощью CSS-классов, которые подключаются вручную к HTML-элементам; или с помощью JS-библиотеки jQuery. В этой статье описаны оба приема уипользования библиотеки Animate.css.
layout: post
permalink: /%d0%b1%d0%b8%d0%b1%d0%bb%d0%b8%d0%be%d1%82%d0%b5%d0%ba%d0%b0-animate-css/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 7
ratings_score:
  - 34
ratings_average:
  - 4.86
categories:
  - Статьи по CSS
tags:
  - animate.css
---
В готовом шаблоне одного фрилансера встретил использование Animate.css &#8211; библиотеки CSS3-эффектов, созданной на самом же CSS3. Ранее я уже встречал упоминание об этой библиотеке &#8211; [Easy CSS3 Animation with Animate.css][1]. Вот теперь пришла пора познакомиться с нею детально, что называется &#8211; на практике.

Кстати, официальная страница этого проекта расположена здесь &#8211; [Animate.css][2]. На ней можно посмотреть все возможные для этой библиотеки эффекты и подобрать подходящий в выпадающем списке.

Откровенно говоря, я приготовился к обстоятельному изучению этой библиотеки, но **все оказалось предельно просто**. Все, что нужно для подключения Animate.css &#8211; это скачать полную версию по ссылке [Download Animate.css][3]. Или же перейти на GitHub &#8211; [View on GitHub][4], чтобы выбрать сжатую (`animate.min.css`) или несжатую (`animate.css`) версию библиотеки.

### Подключение Animate.css

Для подключения библиотеки Animate.css в готовый HTML-проект, достаточно подключить в &#8220;шапке&#8221; документа скачанный CSS-файл `animate.css`:

<pre></pre>

И это все! Больше никаких действий не потребуется &#8211; все остальные манипуляции нужно выполнять в HTML-коде, **добавляя необходимые CSS-классы** из библиотеки Animate.css к нужным HTML-элементам.

### Добавление CSS-классов из Animate.css

Первое, что нужно помнить &#8211; для нужного HTML-элемента необходимо добавить **обязательный класс** `.animated`. CSS-расшифровка этого класса также предельно проста:

<pre>.animated {
    -webkit-animation-duration: 1s;
    animation-duration: 1s;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
  }
  </pre>

Второе &#8211; на [странице проекта][2] подбираем для себя нужный\понравившийся эффект, запоминаем имя (пусть в данном случае это будет `bounceIn`) этого эффекта и добавляем его в качестве имени класса к HTML-элементу, у которого уже есть класс `.animated` (вспоминаем основы CSS &#8211; такая конструкция называется *мультиклассовостью*):

<pre><h1 class="animated bounceIn">
  Animate.css
</h1>
  </pre>

Все &#8211; можно проверять работу библиотеки Animate.css.

### Использование jQuery c Animate.css

Если в проекте используется библиотека jQuery (*а она применяется почти всегда*), то применение библиотеки Animate.css еще больше упрощается, а HTML-разметка **делается семантичной**. Для этого подключаю библиотеку jQuery:

<pre><!--  SCRIPTS  -->
  
  
  </pre>

&#8230; и прописываю в скрипте инициализации `animate_me.js`:

<pre>$(document).ready(function() {
    $('h2').addClass('animated bounceInLeft');
  })
  </pre>

Вуаля &#8211; все отлично работает!

Можно немного **усложнить задачу** и добавить с помощью Jquery событие `hover` к элементу `img`, затем &#8220;повесить&#8221; на него класс анимации `rotateIn` и `animated` из библиотеки Animate.css:

<pre>&lt;figure>
    <img src="images/caramel.jpg" width="800" height="504" alt="Animated Image" />
  &lt;/figure>

  $(document).ready(function() {
    $('figure img').hover(
    function() {
      $(this).addClass('animated rotateIn');
    },
    function() {
      $(this).removeClass('animated rotateIn');
    }
   )})
  </pre>

### Управление задержкой анимации

Можно управлять **задержкой анимации** и **скоростью анимации**, изменив значения в классе `.animated`. Например, с `animation-duration: 1s` на `animation-duration: .4s;`:

<pre>.animated {
    -webkit-animation-duration: .4s;
    animation-duration: .4s;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
  }
  </pre>

### Полный код примера на Animate.css

Полный код рассмотренного в этой статье примера привожу ниже.

**HTML-код:**

<pre>

    

<h1 class="animated bounceIn">
  Animate.css
</h1>
    

<h2>
  animate me with jquery!
</h2>

    &lt;figure>
      

<img src="images/caramel.jpg" width="800" height="504" alt="Animated Image" />
    &lt;/figure>

    <!--  SCRIPTS  -->
    
    
  
  </pre>

**SCSS-код:**

<pre>$color: #778899;

  h1,h2,figure{
    margin: 50px auto 0;
    text-align: center;
  }

  h1{
    font: normal 72px/1.3 Georgia, sans-serif;
    color: darken($color,10%);
  }

  h2{
    font: normal 56px/1.3 Georgia, sans-serif;
    color: lighten($color,5%);
    text-transform: capitalize;
  }

  figure img:hover{
    cursor: pointer;
  }
  </pre>

**JS-код:**

<pre>$(document).ready(function() {
    $('h2').addClass('animated bounceInLeft');
    $('figure img').hover(
    function() {
      $(this).addClass('animated rotateIn');
    },
    function() {
      $(this).removeClass('animated rotateIn');
    }
   )})
  </pre><figure id="attachment_1522" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/animate.css-600x564.png" alt="Библиотека Animate.css в действии" width="600" height="564" class="size-medium wp-image-1522" />][5]<figcaption class="wp-caption-text">Библиотека Animate.css в действии</figcaption></figure> 

На этом все.

Оцените статью:  
<span id="post-ratings-1520" class="post-ratings" data-nonce="40d270eac3"><img id="rating_1520_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1520, 1, '1 Star');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1520_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1520, 2, '2 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1520_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1520, 3, '3 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1520_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1520, 4, '4 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1520_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1520, 5, '5 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>7</strong> votes, average: <strong>4,86</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1520_text"></span></span><span id="post-ratings-1520-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://www.sitepoint.com/animate-css-css3-animation/ "Easy CSS3 Animation with Animate.css"
 [2]: http://daneden.github.io/animate.css/ "Animate.css"
 [3]: https://raw.github.com/daneden/animate.css/master/animate.css "Download Animate.css"
 [4]: http://github.com/daneden/animate.css "View on GitHub"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/07/animate.css.png