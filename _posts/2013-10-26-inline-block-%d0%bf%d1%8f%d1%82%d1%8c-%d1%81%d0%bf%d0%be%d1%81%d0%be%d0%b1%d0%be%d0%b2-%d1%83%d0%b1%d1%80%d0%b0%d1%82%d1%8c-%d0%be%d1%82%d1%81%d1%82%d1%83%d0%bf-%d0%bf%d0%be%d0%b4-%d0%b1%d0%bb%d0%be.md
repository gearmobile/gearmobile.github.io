---
title: 'Элемент inline &#8211; пять способов убрать отступ'
author: gearmobile
layout: post
permalink: /inline-block-%d0%bf%d1%8f%d1%82%d1%8c-%d1%81%d0%bf%d0%be%d1%81%d0%be%d0%b1%d0%be%d0%b2-%d1%83%d0%b1%d1%80%d0%b0%d1%82%d1%8c-%d0%be%d1%82%d1%81%d1%82%d1%83%d0%bf-%d0%bf%d0%be%d0%b4-%d0%b1%d0%bb%d0%be/
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - inline
---
При оборачивании изображения в блок div внизу картинки возникает странный отступ. Появляется он потому, что элемент img является строчным (inline). При верстке часто возникает задача его убрать, так как он лишний и только портит дизайн. Решений данного вопроса существует несколько. С тремя из них я был уже знаком благодаря замечательному ресурсу для верстальщиков &#8211; xiper.net. А вот на сайте htmlbook.ru Влада Мержевича в разделе &#8220;Практикум&#8221; узнал, что таких способ не три, а пять. С задачкой справился, а решения захотел поместить у себя.

### Итак, пять способов убрать отступ под картинкой

Создаем блок div с классом image, для которого назначаем ширину, центрирование и границу для наглядности. Внутрь блока div.image помещаем картинку.

HTML:

<pre>&lt;div class="image"&gt;
        &lt;img src="img/charlize_theron.jpg" width="307" height="230" alt="Charlize Theron"&gt;
      &lt;/div&gt;
</pre>

CSS:

<pre>.image{border: 2px solid #000; width: 307px; margin: 0 auto}
</pre></p> 

Видим этот отступ под изображением:<figure id="attachment_70" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_origin-600x379.png" alt="Изображение с отступом" width="600" height="379" class="size-medium wp-image-70" />][1]<figcaption class="wp-caption-text">Изображение с отступом</figcaption></figure> 

И пробуем пятью различными способами убрать этот отступ.

### 1. Сделать элемент img блочным<figure id="attachment_71" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_block-600x354.png" alt="Сделать элемент inline-block блочным - display: block" width="600" height="354" class="size-medium wp-image-71" />][2]<figcaption class="wp-caption-text">Сделать элемент inline блочным &#8211; display: block</figcaption></figure> 

CSS:

<pre>.block{display: block;}
</pre>

### 2. Задать вертикальное выравнивание

Так как элемент img является строчным (inline), то к нему применимо свойство vertical-align, как к любому строчному элементу. Мне такой способ нравиться больше всего:<figure id="attachment_72" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_vertical-align-600x354.png" alt="Элемент inline-block - присвоить vertical-align: top" width="600" height="354" class="size-medium wp-image-72" />][3]<figcaption class="wp-caption-text">Элемент inline &#8211; присвоить vertical-align: top</figcaption></figure> 

CSS:

<pre>.vertical{vertical-align: top;}
</pre>

### 3. Сделать элемент плавающим через float

Задать для элемента img свойство float: left или float: right. Если элемент делается плавающим через float, то из строчного (inline) он становится блочным (block). И отступ также пропадает. Только надо не забыть добавить для контейнера div.image свойство overflow: hidden, иначе пропадет граница вокруг изображения. Что и понятно, так как при float: left или float: right элемент &#8220;вырывается&#8221; из общего потока, становится плавающим:<figure id="attachment_73" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_float-600x354.png" alt="Элемент inline-block - присвоить float: left" width="600" height="354" class="size-medium wp-image-73" />][4]<figcaption class="wp-caption-text">Элемент inline &#8211; присвоить float: left</figcaption></figure> 

CSS:

<pre>.float{float: left;}
</pre>

### 4. Сделать картинку таблицей

Для изображения задать свойство display: table.<figure id="attachment_74" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_table-600x354.png" alt="Элемент inline-block - присвоить display: table" width="600" height="354" class="size-medium wp-image-74" />][5]<figcaption class="wp-caption-text">Элемент inline &#8211; присвоить display: table</figcaption></figure> 

CSS:

<pre>.table{display: table;}
  </pre>

### 5. Задать высоту для блока

Для блока-контейнера div.image жестко задать высоту, равную высоте изображения. В моем случае высота картинки равна 230 пикселей, поэтому и для блока-обертки задаю такую же &#8211; 230 пикселей:<figure id="attachment_75" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_width-600x354.png" alt="Элемент inline-block - присвоить width" width="600" height="354" class="size-medium wp-image-75" />][6]<figcaption class="wp-caption-text">Элемент inline &#8211; присвоить width</figcaption></figure> 

CSS:

<pre>.height{height: 230px}
</pre>

Все пять способов проверены мною и должны работать в реальности.

Оцените статью:  
<span id="post-ratings-67" class="post-ratings" data-nonce="a1deb8b43f"><img id="rating_67_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(67, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_67_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(67, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_67_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(67, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_67_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(67, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_67_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(67, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_67_text"></span></span><span id="post-ratings-67-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_origin.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_block.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_vertical-align.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_float.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_table.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/10/inline-block_width.png