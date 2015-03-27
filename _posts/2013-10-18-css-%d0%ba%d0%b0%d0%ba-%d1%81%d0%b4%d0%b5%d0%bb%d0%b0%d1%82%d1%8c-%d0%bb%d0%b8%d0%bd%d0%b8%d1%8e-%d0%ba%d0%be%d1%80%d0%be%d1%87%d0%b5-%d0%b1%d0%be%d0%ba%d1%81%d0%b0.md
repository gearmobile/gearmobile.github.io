---
title: 'CSS &#8211; как сделать линию короче бокса'
author: gearmobile
layout: post
permalink: /css-%d0%ba%d0%b0%d0%ba-%d1%81%d0%b4%d0%b5%d0%bb%d0%b0%d1%82%d1%8c-%d0%bb%d0%b8%d0%bd%d0%b8%d1%8e-%d0%ba%d0%be%d1%80%d0%be%d1%87%d0%b5-%d0%b1%d0%be%d0%ba%d1%81%d0%b0/
ratings_users:
  - 3
ratings_score:
  - 13
ratings_average:
  - 4.33
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - :after
  - css
---
При верстке макета сайта, кстати, совсем несложного, возник вопрос. Заключается он в том, имеется информационная часть, разбитая на две колонки. Каждая из колонок также разделена на отдельные секции &#8211; посты. Для колонок и постов на макете задуманы дизайнером декоративные линии-разделители.

Проблемы с созданием таких линий, в принципе, нет никакой. Их можно легко создать с помощью стилевого правила border-bottom и border-right. Или же с помощью правил border-right и элемента hr.

Но вопрос заключается в том, что декоративные линии на макете короче, чем высота колонки или ширина поста. То есть, получается, что border должен быть короче, чем бокс:<figure id="attachment_167" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-lines-600x395.png" alt="Декоративные линии короче, чем контент" width="600" height="395" class="size-medium wp-image-167" />][1]<figcaption class="wp-caption-text">Декоративные линии короче, чем контент</figcaption></figure> 

Как же поступить в данном случае? Скажем так, обычными способами CSS решить такой вопрос невозможно. Но решение было найдено с помощью форума htmlbook.

В данном случае можно выйти из положения с помощью псевдокласса :after. Для наглядности представим такой пример.

Создаем слой с контентом:

<pre>text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text
</pre>

И пропишем для него стилевые правила:

<pre>div {
    width: 300px;
    position: relative;
  }
</pre>

Как видим, их не так уж и много. Задаем ширину блока и устанавливаем для него относительное позициоирование. Затем для созданного нами бокса создаем псевдокласс :after и прописываем для него свойства:

<pre>div:after {
    content: "";
    position: absolute;
    top: 30px;
    right: -10px;
    bottom: 30px;
    border-left: 1px solid #000;
  }
</pre>

Немного распишем, что да как в этом коде.

Внутри простого блока после его содержимого создается псевдоблок с абсолютным позиционированием, для которого устанавливаются координаты top и bottom (благодаря двум последним он растягивается, так как создаются верхняя и нижняя координата для границы) и для этого блока создается только левая граница border-left со свойствами: 1px сплошного черного цвета.

Оцените статью:  
<span id="post-ratings-166" class="post-ratings" data-nonce="98de2eeba3"><img id="rating_166_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(166, 1, '1 Star');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_166_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(166, 2, '2 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_166_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(166, 3, '3 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_166_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(166, 4, '4 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_166_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(166, 5, '5 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>4,33</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_166_text"></span></span><span id="post-ratings-166-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/css-lines.png