---
title: Маркированный список ul в две колонки через CSS2
author: gearmobile
layout: post
permalink: /%d0%bc%d0%b0%d1%80%d0%ba%d0%b8%d1%80%d0%be%d0%b2%d0%b0%d0%bd%d0%bd%d1%8b%d0%b9-%d1%81%d0%bf%d0%b8%d1%81%d0%be%d0%ba-ul-%d0%b2-%d0%b4%d0%b2%d0%b5-%d0%ba%d0%be%d0%bb%d0%be%d0%bd%d0%ba%d0%b8-%d1%87%d0%b5/
ratings_users:
  - 8
ratings_score:
  - 27
ratings_average:
  - 3.38
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - css2
---
Достаточно интересный способ организации обычного маркированного списка в две колонки. Имеется определенное количество элементов li списка ul. Нужно организовать все li в две колонки. Первое, что приходит на ум &#8211; это воспользоваться новыми правилами CSS3. Но проблема в том, они новые и не всеми браузерами поддерживаются. Тогда смысл их применять? Но можно воспользоваться CSS2 и этот способ был случайно мною &#8220;подсмотрен&#8221; на сайте Loco.ru у автора dIrm. Мною этот способ был немного доработан и помещен у себя в качестве копилки.

Итак, имеется обычный маркированный список в виде HTML-разметки. Количество элементов li я специально сделал нечетным:

<pre><ul>
  <li>
    Колонка 1
  </li>
        
  
  <li>
    Колонка 2
  </li>
        
  
  <li>
    Колонка 3
  </li>
        
  
  <li>
    Колонка 4
  </li>
        
  
  <li>
    Колонка 5
  </li>
        
  
  <li>
    Колонка 6
  </li>
        
  
  <li>
    Колонка 7
  </li>
        
  
  <li>
    Колонка 8
  </li>
        
  
  <li>
    Колонка 9
  </li>
        
  
  <li>
    Колонка 10
  </li>
        
  
  <li>
    Колонка 11
  </li>
      
</ul>
  </pre>

Сделаем CSS-стилизацию списка, ничем не примечательную. Класс `.clearfix` добавим в HTML-разметку для элемента ul &#8211; это классическая очистка потока для плавающих потомков внутри блока-родителя. Элементы li у нас будут плавать внутри ul:

<pre>ul{
      list-style-type: none;
      width: 398px;
      margin: 100px auto;
      border: 1px solid #000;
      font: bold italic 16px/30px Georgia, serif;
      color: #fff;
      text-shadow: 1px 1px 1px rgba(0,0,0,.8);
    }
    .clearfix:before,
    .clearfix:after{
      content: "";
      display: table;
    }
    .clearfix:after{
      clear: both;
    }
  </pre>

Вот теперь немного интереснее, когда приступим к элементу li. Вся &#8220;фишка&#8221; в организации их в два столбца благодаря двум CSS-правилам &#8211; `display: block` и `width: 45%`. Все элементы сделаем плавающими влево `float: left`, поэтому CSS-правило `display: block` можно опустить за ненадобностью, но оставим его для наглядности примера. Получается, что каждый из элементов li является блочным, с фиксированной шириной и плавает влево. В результате все эти элементы располагаются &#8220;по порядку&#8221;. &#8220;Колонка 1&#8243; в левом верхнем углу, следом за ним &#8211; &#8220;Колонка 2&#8243;. &#8220;Колонка 3&#8243; не вмещается по ширине в область блока-родителя, поэтому располагается под &#8220;Колонка 1&#8243;. Далее &#8211; опять все по порядку. Три правила `padding-bottom: 10px`, `text-align: center`, `background-color: #556677` &#8211; для красоты добавляем:

<pre>ul li{
      display: block;
      float: left;
      width: 45%;
      padding-bottom: 10px;
      text-align: center;
      background-color: #556677;
    }
  </pre>

Ну и в конце еще несколько штрихов для придания полной иллюзии двухколоночного текста. Здесь воспользуемся правилом nth-child с аргументом even, чтобы избежать дополнительной нагрузки на разметку в виде классов, которые придется добавлять в противном случае:

<pre>li:nth-child(even){
      margin-left: 10%;
      background-color: #667788;
    }
  </pre>

Демо-пример можно посмотреть здесь &#8211; &#8220;<a href="http://demo.zencoder.ru/" title="Elements li in two columns" target="_blank">Elements li in two columns</a>&#8220;. Исходные файлы скачать &#8211; &#8220;<a href="https://dl.dropboxusercontent.com/u/1093631/Elements%20li%20in%20two%20columns.zip" title="Elements li in two columns" target="_blank">Elements li in two columns</a>&#8220;.

Оцените статью:  
<span id="post-ratings-558" class="post-ratings" data-nonce="abff38e56f"><img id="rating_558_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(558, 1, '1 Star');" onmouseout="ratings_off(3.4, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_558_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(558, 2, '2 Stars');" onmouseout="ratings_off(3.4, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_558_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(558, 3, '3 Stars');" onmouseout="ratings_off(3.4, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_558_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(558, 4, '4 Stars');" onmouseout="ratings_off(3.4, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_558_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(558, 5, '5 Stars');" onmouseout="ratings_off(3.4, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>8</strong> votes, average: <strong>3,38</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_558_text"></span></span><span id="post-ratings-558-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>