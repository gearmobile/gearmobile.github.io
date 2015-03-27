---
title: Плагин Smooth Scroll
author: gearmobile
excerpt: Плагин Smooth Scroll предназначен для создания плавного скроллинга (прокрутки) HTML-страницы. Скрипт очень прост в установке и настройке, имеет маленький размер. Плюсы использования плагина Smooth Scroll в улучшении юзабилити страницы (сайта в целом).
layout: post
permalink: /%d0%bf%d0%bb%d0%b0%d0%b3%d0%b8%d0%bd-smooth-scroll/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
categories:
  - 'Javascript &amp; jQuery'
tags:
  - smooth scroll
---
Обзор краткий такого же небольшого плагина Smooth Scroll, написанного под библиотеку jQuery. Этот скрипт предназначен только для одной цели &#8211; плавного скроллинга (*прокрутки*) страницы. Благодаря этому **улучшается юзабилити** страницы и сайта в целом, так как нет резких скачков при переходе по ссылкам.

### Подключение плагина Smooth Scroll

Подключение Smooth Scroll к HTML-странице производится как обычно:

<pre><!--  SCRIPTS  -->
  
  
  
  ...
  </pre>

&#8230; где **первая строка** &#8211; это библиотека jQuery, **вторая строка** &#8211; плагин Smooth Scroll, **третья строка** &#8211; файл инициализации плагина Smooth Scroll.

### Инициализация Smooth Scroll

Для того, чтобы заработал плагин Smooth Scroll и на странице появилась плавная прокрутка, нужно в js-файле скрипта прописать строки:

<pre>$(document).ready(function(){
    $('a').smoothScroll();
  });
  </pre>

&#8230; то есть &#8211; всем ссылкам страницы присвоить метод `smoothScroll()`, что дает **плавный скроллинг**. В принципе, этого достаточно &#8211; больше ничего и не надо.

### Варианты выборки в Smooth Scroll

Помимо показанной выше строчки, скрипт Smooth Scroll имеет несколько других вариантов режима работы. Другими словами, эти режимы работы &#8211; все навсего усложненный первый вариант, вариации на тему выборки HTML-элемента в библиотеке jQuery.

Примеры выборок взяты мною из файла `readme.md`, переводить их мне совсем не хочется; да и нет в этом необходимости &#8211; все понятно даже по коду:

  * Allows for easy implementation of smooth scrolling for same-page links.
  * Works like this: `$('a').smoothScroll();`
  * Specify a containing element if you want: `$('#container a').smoothScroll();`
  * Exclude links if they are within a containing element: `$('#container a').smoothScroll({excludeWithin: ['.container2']});`
  * Exclude links if they match certain conditions: `$('a').smoothScroll({exclude: ['.rough','#chunky']});`
  * Adjust where the scrolling stops: `$('.backtotop').smoothScroll({offset: -100});`
  * Add a callback function that is triggered before the scroll starts: \`$(&#8216;a&#8217;).smoothScroll({beforeScroll: function() { alert(&#8216;ready to go!&#8217;); }});
  * Add a callback function that is triggered after the scroll is complete: `$('a').smoothScroll({afterScroll: function() { alert('we made it!'); }});`

### Пример работы Smooth Scroll

Ниже привожу пример HTML, SCSS и JS-кода, на котором проходил &#8220;испытание&#8221; плагин Smooth Scroll у меня, в моей &#8220;лаборатории&#8221;.

HTML-код:

<pre>

    

<h1 class="head">
  smooth scroll plugin
</h1>

    

<ul class="scroll">
  <li>
    <a href="#h1">header 1</a>
  </li>
        
  
  <li>
    <a href="#h2">header 2</a>
  </li>
        
  
  <li>
    <a href="#h3">header 3</a>
  </li>
        
  
  <li>
    <a href="#h4">header 4</a>
  </li>
        
  
  <li>
    <a href="#h5">header 5</a>
  </li>
      
</ul>

    

<h1>
  header 1
</h1>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h2>
  header 2
</h2>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h3 id="h3">
  header 3
</h3>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h4>
  header 4
</h4>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5 id="h5">
  header 5
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 6
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 7
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h1>
  header 1
</h1>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h2 id="h2">
  header 2
</h2>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h3>
  header 3
</h3>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h4>
  header 4
</h4>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 5
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 6
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 7
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h1 id="h1">
  header 1
</h1>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h2>
  header 2
</h2>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h3>
  header 3
</h3>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h4 id="h4">
  header 4
</h4>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 5
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 6
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<h5>
  header 7
</h5>

    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.
</p>
    

<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?
</p>

    

<!--  SCRIPTS  -->
    
    
    

  
  </pre>

SCSS-код:

<pre>$color: #778899;

  h1,h2,h3,h4,h5{
    text-transform: uppercase;
    font-family: Georgia, sans-serif;
    text-align: center;
  }

  h1{
    font-size: 36px;
    color: $color;
  }
  h2{
    font-size: 32px;
    color: lighten($color,5%);
  }
  h3{
    font-size: 28px;
    color: lighten($color,10%);
  }
  h4{
    font-size: 24px;
    color: lighten($color,15%);
  }
  h5{
    font-size: 24px;
    color: lighten($color,20%);
  }
  h6{
    font-size: 20px;
    color: lighten($color,25%);
  }
  h7{
    font-size: 18px;
    color: lighten($color,30%);
  }

  .head{
    text-transform: capitalize;
    font-size: 48px;
    color: darken($color,5%);
  }

  .scroll{
    list-style-type: none;
    padding: 0 0 0 100px;
    li{
      margin-bottom: 10px;
      a{
        text-transform: capitalize;
        text-decoration: none;
        color: darken($color,10%);
        &#038;:hover{
          color: darken($color,15%);
        }
      }
    }
  }
  </pre>

JS-код:

<pre>$(document).ready(function(){
    $('a').smoothScroll();
  });
  </pre>

Оцените статью:  
<span id="post-ratings-1527" class="post-ratings" data-nonce="eb6aced7cb"><img id="rating_1527_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1527, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1527_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1527, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1527_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1527, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1527_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1527, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1527_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1527, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1527_text"></span></span><span id="post-ratings-1527-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>