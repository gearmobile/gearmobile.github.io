---
title: 'Parallax.js &#8211; создаем простой parallax'
author: gearmobile
excerpt: Создание простого эффекта parallax для страницы с помощью скрипта parallax.js. Скрипт не требует библиотеки jQuery. Разметка для скрипта parallax.js проста.
layout: post
permalink: /parallax-js/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 11
ratings_average:
  - 3.67
categories:
  - 'Javascript &amp; jQuery'
tags:
  - parallax.js
---
Небольшой обзор новой для меня темы &#8211; создание эффекта parallax на странице сайта. Вместе с вами буду учиться создавать такой эффект и начну с самого простого &#8211; Parallax.js.

Чтобы посмотреть, что примерно мы должны в результате получить, посмотрим на домашнюю страницу этого проекта &#8211; [Parallax.js][1]. Исходный код скрипта и документация расположена на GitHub &#8211; [Parallax.js][2]

### Кратко о parallax

Что такое parallax как эффект сам по себе, хорошо видно на самой страничке и расписывать его я не буду. В Интернет есть лучшее и более подробное описание эффекта parallax. Единственное, что можно сказать по поводу parallax &#8211; появился он в основном как необходимость, дань моде. Своим существованием практически полностью обязан популярным на сегодняшний день landing page и призван скрасить и разнообразить их относительную монотонность.

Способов реализации parallax на сегодня сушествует множество. Но практически все они основаны на одном принципе &#8211; изменении скорости прокрутки фонового изображения на странице относительно других объектов на ней (*поправьте меня, если я неправ*).

Одним из преимуществ метода на основе скрипта Parallax.js является то, что в этом случае **не требуется библиотеки jQuery**. Скрипт может работать и с ней, но ее присутствие совсем необязательно. Получается **выгода в весе страницы и скорости ее загрузки** в браузере.

### Parallax.js &#8211; начальная разметка

HTML-разметка для нашего будущего parallax **удивительно простая** &#8211; это маркированный список `ul` с идентификатором (*имя его произвольное*) и элементами списка `li` (*имя класса обязательно и неизменно*).

Еще одним обязательным атрибутом для элементов списка `li` является атрибут `data-depth`, у которого значение может меняться в диапазоне от 0 до 1. Чем выше значение в 1, тем выше скорость перемещения объекта на странице.

Внутрь элементов списка помещается изображение, которое будет анимироваться с помощью эффекта parallax.

Ниже приведен пример такой разметки:

<pre><ul id="scene">
  <li class="layer" data-depth="0.10">
    <img src="images/one.png" height="100" width="100" alt="Image" />
  </li>
    
  
  <li class="layer" data-depth="0.80">
    <img src="images/two.png" height="100" width="100" alt="Image" />
  </li>
    
  
  <li class="layer" data-depth="0.20">
    <img src="images/three.png" height="100" width="100" alt="Image" />
  </li>
    
  
  <li class="layer" data-depth="0.80">
    <img src="images/four.png" height="100" width="100" alt="Image" />
  </li>
  
</ul>
</pre>

### Parallax.js &#8211; стилизация parallax

Произведем небольшую стилизацию нашего будущего parallax с помощью Sass/Compass. Для элемента `ul` добавим фоновое изображение, чтобы был лучше виден эффект parallax.

<pre>@import "compass/";
@import "compass/reset";

#scene{
  width: 95%;
  margin: 20px auto 0;
  min-height: 775px;
  background: url(../images/bg.jpg) 0 0 no-repeat;
  img{
    display: inline-block;
    width: 100px;
    height: 100px;
    @include border-radius(50%);
  }
  img[src="images/one.png"]{
    margin: 200px 0 0 200px;
  }
  img[src="images/two.png"]{
    margin: 200px 0 0 1000px;
  }
  img[src="images/three.png"]{
    margin: 500px 0 0 700px;
  }
  img[src="images/four.png"]{
    margin: 600px 0 0 300px;
  }
}
</pre>

### Parallax.js &#8211; добавляем javascript

Наш parallax почти готов &#8211; осталось &#8220;вдохнуть в него жизнь&#8221; с помощью Javascript.

Добавляем в конец HTML-документа всего две строчки:

<pre></pre>

Тут все просто. Первой строкой подключается файл скрипта Parallax.js. Второй строкой сначала в теле документа отыскивается элемент с идентификатором `scene`, который помещается внутрь переменной `scene`. Затем создается новый экземпляр `parallax` объекта Parallax и ему передается в качестве аргумента эта переменная `scene`.

Все &#8211; смотрим результат:<figure id="attachment_1935" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/ParallaxJS-600x439.png" alt="Готовый эффект на Parallax.js" width="600" height="439" class="size-medium wp-image-1935" />][3]<figcaption class="wp-caption-text">Готовый эффект на Parallax.js</figcaption></figure> 

Достаточно подвигать мышью над фотографией красавчика на заднем плане, чтобы увидеть, как разноцветные кружки перемещаются с разной скоростью.

Мы получили эффект parallax.

Ниже приведен полный код HTML и CSS рассмотренного нами примера:

HTML:

<pre>






<ul id="scene">
  <li class="layer" data-depth="0.10">
    &lt;img src="images/one.png" height="100" width="100" alt="Image"
  </li>
    
  
  <li class="layer" data-depth="0.80">
    &lt;img src="images/two.png" height="100" width="100" alt="Image"
  </li>
    
  
  <li class="layer" data-depth="0.20">
    &lt;img src="images/three.png" height="100" width="100" alt="Image"
  </li>
    
  
  <li class="layer" data-depth="0.80">
    &lt;img src="images/four.png" height="100" width="100" alt="Image"
  </li>
  
</ul>



<!-- Scripts -->
 
 


</pre></p> 

CSS:

<pre>@import "compass";
@import "compass/reset";

scene{
width: 95%;
 margin: 20px auto 0;
 min-height: 775px;
 background: url(../images/bg.jpg) 0 0 no-repeat;
 img{
 display: inline-block;
 width: 100px;
 height: 100px;
 @include border-radius(50%);
 }
 img[src="images/one.png"]{
 margin: 200px 0 0 200px;
 }
 img[src="images/two.png"]{
 margin: 200px 0 0 1000px;
 }
 img[src="images/three.png"]{
 margin: 500px 0 0 700px;
 }
 img[src="images/four.png"]{
 margin: 600px 0 0 300px;
 }
}
</pre></p> 

Полный исходный код примера можно посмотреть на GitHub &#8211; [Parallax.js][4]

Оцените статью:  
<span id="post-ratings-1934" class="post-ratings" data-nonce="8b7ed7b7a3"><img id="rating_1934_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1934, 1, '1 Star');" onmouseout="ratings_off(3.7, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1934_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1934, 2, '2 Stars');" onmouseout="ratings_off(3.7, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1934_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1934, 3, '3 Stars');" onmouseout="ratings_off(3.7, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1934_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1934, 4, '4 Stars');" onmouseout="ratings_off(3.7, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1934_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1934, 5, '5 Stars');" onmouseout="ratings_off(3.7, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>3,67</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1934_text"></span></span><span id="post-ratings-1934-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://matthew.wagerfield.com/parallax/ "Parallax.js"
 [2]: https://github.com/wagerfield/parallax "Parallax.js"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/11/ParallaxJS.png
 [4]: https://github.com/gearmobile/zencoder/tree/master/parallaxjs "Parallax.js"