---
title: 'Parallax.js &#8211; создаем parallax со скроллингом'
author: gearmobile
excerpt: Создание эффекта parallax с вертикальным скроллингом с помощью скрипта Parallax.js. Скрипт имеет небольшое число настроек и требует незамысловатой HTML-разметки. С помощью него можно легко и быстро создать parallax.
layout: post
permalink: /parallax-js-vertical-scrolling/
ratings_users:
  - 2
ratings_score:
  - 9
ratings_average:
  - 4.5
cleanretina_sidebarlayout:
  - default
categories:
  - 'Javascript &amp; jQuery'
tags:
  - parallax.js
---
В данном примере рассмотрим создание parallax **с эффектом вертикального скроллинга**. Это самый популярный вид parallax&#8217;а для страниц типа Landing Page.

Создавать эффект будет с помощью скрипта Parallax.js. По странному стечению обстоятельств данный скрипт имеет точно такое же имя, что и скрипт из предыдущего примера &#8211; &#8220;[Parallax.js &#8211; создаем простой parallax][1]&#8221;. Однако, это разные скрипты и авторы у них разные; данный скрипт расположен на странице GitHub по адресу &#8211; [Parallax.js][2].

Домашняя страничка скрипта выполнена также с эффектом parallax &#8211; [Simple Parallax Scrolling][3].

### Parallax.js &#8211; создаем HTML-разметку

Разметка для скрипта Parallax.js проста. Это обычный блок, который может быть `div`, `section` или что-либо еще. Обязательным условием является подключение для блока класса `class="parallax-window"` и двух data-атрибутов: `data-parallax="scroll"` и `data-image-src="images/one.jpg"`. Второй атрибут в качестве своего значения имеет **относительный путь к файлу изображения**, которое будет устанавливаться в виде фона.

В дополнение можно задать еще несколько атрибутов для **ускорения загрузки изображений браузером**:

  * data-natural-width &#8211; реальная ширина изображения
  * data-natural-height &#8211; реальная высота изображения

Ниже приведу созданные мною четыре блока `section` с содержимым:

<pre><!-- begin one -->
  &lt;section data-parallax="scroll" data-image-src="images/one.jpg" class="parallax-window">
    

<div class="wrap one">
  <h1>
    Welcome to Parallax!
  </h1>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Temporibus consequatur, nulla neque voluptatum deserunt at voluptatibus eos. Magni sapiente rem, suscipit assumenda provident, quaerat doloribus libero? Eaque doloremque, quo sequi!
  </p>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sint nemo cum, dignissimos blanditiis iusto quasi, quis! Ducimus aperiam sunt libero deleniti numquam rerum esse architecto, officiis amet, officia recusandae aut.
  </p>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Itaque reiciendis vitae, amet! Quas saepe consequuntur, nisi quia, cupiditate dignissimos laborum incidunt soluta repellat, libero id quibusdam mollitia maiores omnis tempore.
  </p>
      
</div>
  &lt;/section>


<!-- end one -->



<!-- begin two -->
  &lt;section data-parallax="scroll" data-image-src="images/two.jpg" class="parallax-window">
  

<div class="wrap two">
  <h2>
    Parallax is great!
  </h2>
      
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Modi accusamus deserunt ipsum nesciunt odit vero corporis eaque, quibusdam, enim, beatae, repellendus iusto. Amet corporis beatae, inventore officiis est aut. Ab!
  </p>
      
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Maxime possimus sint a facere dignissimos! Labore at, beatae consequuntur corporis perspiciatis! Asperiores illum esse repellat veniam vero totam debitis! Quos, consectetur.
  </p>
      
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nulla, totam maxime dolorum similique, ipsa a. Ea illo eligendi, ex, officia id eum sit sint nobis aperiam, error nihil ab dolorum.
  </p>
    
</div>
  &lt;/section>


<!-- end two -->



<!-- begin three -->
  &lt;section data-parallax="scroll" data-image-src="images/three.jpg" class="parallax-window">
    

<div class="wrap three">
  <h3>
    Parallax is easy!
  </h3>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque quia ex doloremque et, eum soluta culpa ipsum placeat consectetur, error at, accusamus iure! Doloribus corporis, earum quo modi omnis hic.
  </p>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cum ab distinctio omnis repellendus exercitationem maiores ad sed, deleniti dolorem tempore praesentium nobis suscipit nihil quidem qui nostrum debitis ipsam culpa.
  </p>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Impedit, repellendus, qui. Aspernatur reiciendis eligendi, totam eaque iusto illo officia. Facere dicta harum, dolore sit perferendis in neque mollitia eligendi dignissimos?
  </p>
      
</div>
  &lt;/section>


<!-- end three -->



<!-- begin four -->
  &lt;section data-parallax="scroll" data-image-src="images/four.jpg" class="parallax-window">
    

<div class="wrap">
  <h4>
    Let's start use it!
  </h4>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eius ab voluptates alias corporis, laborum provident corrupti assumenda dignissimos vel repellendus obcaecati, aspernatur earum ipsum rem. Voluptatum ipsum nostrum in! Rerum.
  </p>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reprehenderit alias illum minus asperiores culpa, modi veritatis quibusdam, aperiam accusantium repellendus at possimus qui cupiditate dolorem quod accusamus a. Mollitia, repudiandae.
  </p>
        
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio quo nulla officia sapiente a tenetur maxime sunt mollitia accusantium aut, eius minus maiores fugit necessitatibus obcaecati ex eos quibusdam sequi.
  </p>
      
</div>
  &lt;/section>


<!-- end four -->
</pre>

### Parallax.js &#8211; стилизация страницы

Стилизацию страницы буду выполнять на Sass/Compass с использованием вертикального ритма Vertical Rhythm &#8211; в данном случае он подойдет как раз к месту, как мне кажется:

<pre>@import "compass";
@import "compass/reset";


$base-font-size: 24px;
$base-line-height: 36px;
$rhythm-unit: "rem";
$rem-with-px-fallback: true;

@include establish-baseline;


.parallax-window {
    min-height: 1080px;
    background: transparent;
    .wrap{
      margin-top: 100px;
      text-align: center;
      width: 1200px;
      margin: 0 auto;
      @include leader($lines: 7, $property: padding);
      p{
        @include rhythm-margins;
      }
      h1{
        @include adjust-font-size-to(2.074rem);
      }
      h2{
        @include adjust-font-size-to(1.728rem);
      }
      h3{
        @include adjust-font-size-to(1.44rem);
      }
      h4{
        @include adjust-font-size-to(1.2rem);
      }
      &#038;.one{
        text-align: center;
        color: rgba(255,255,255,.8);
      }
      &#038;.two{
        text-align: left;
        color: rgba(0, 0, 0, .8);
      }
      &#038;.three{
        text-align: right;
        color: rgba(255, 255, 255, .8);
      }
    }
}
</pre>

В этом коде наиболее важными строками являются две &#8211; без них скроллинга не получиться:

<pre>.parallax-window {
    min-height: 1080px;
    background: transparent;
    ...
</pre>

### Parallax.js &#8211; добавление Javascript

Разметка и стили готовы &#8211; осталось подключить скрипт Parallax.js и библиотеку jQuery:

<pre></pre>

jQuery &#8220;забираем&#8221; с Google, а скрипт Parallax.js &#8211; с GitHub-страницы проекта &#8211; [Parallax.js][2]. Все это &#8220;добро&#8221; пихаем в самый низ, подвал HTML-документа &#8211; перед закрывающим тегом `</body>`.

В дальнейшие украшательства вдаваться не буду &#8211; это дело техники. Мне важен сам принцип создания parallax с эффектом вертикального скроллинга.

В принципе, у меня все готово для того, чтобы полюбоваться результатом. Открываю страницу в браузере и любуюсь (не забывая скролить саму страницу):<figure id="attachment_1941" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/ParallaxJX-_Scrolling-600x364.png" alt="Страница на Parallax.js с вертикальным скроллингом" width="600" height="364" class="size-medium wp-image-1941" />][4]<figcaption class="wp-caption-text">Страница на Parallax.js с вертикальным скроллингом</figcaption></figure> 

Отлично! Получился прямо таки совсем неплохой parallax с вертикальным скроллингом <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

Готовый пример со всеми исходниками можно посмотреть на GitHub &#8211; [Parallax.js Scrolling][5].

Оцените статью:  
<span id="post-ratings-1940" class="post-ratings" data-nonce="074ccebc6b"><img id="rating_1940_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1940, 1, '1 Star');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1940_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1940, 2, '2 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1940_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1940, 3, '3 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1940_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1940, 4, '4 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1940_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1940, 5, '5 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>4,50</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1940_text"></span></span><span id="post-ratings-1940-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1934 "Parallax.js - создаем простой parallax"
 [2]: https://github.com/pixelcog/parallax.js/ "Parallax.js"
 [3]: http://pixelcog.com/parallax.js/ "Simple Parallax Scrolling"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/11/ParallaxJX-_Scrolling.png
 [5]: https://github.com/gearmobile/zencoder/tree/master/parallaxjs_scroll "Parallax.js Scrolling"