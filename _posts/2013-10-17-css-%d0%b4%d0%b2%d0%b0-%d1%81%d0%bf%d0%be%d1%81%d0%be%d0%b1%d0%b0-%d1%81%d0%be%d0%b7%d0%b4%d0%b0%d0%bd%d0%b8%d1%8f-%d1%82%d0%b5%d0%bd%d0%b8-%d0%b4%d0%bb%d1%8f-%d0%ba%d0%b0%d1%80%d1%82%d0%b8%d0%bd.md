---
title: 'CSS &#8211; два способа создания тени для картинки'
author: gearmobile
layout: post
permalink: /css-%d0%b4%d0%b2%d0%b0-%d1%81%d0%bf%d0%be%d1%81%d0%be%d0%b1%d0%b0-%d1%81%d0%be%d0%b7%d0%b4%d0%b0%d0%bd%d0%b8%d1%8f-%d1%82%d0%b5%d0%bd%d0%b8-%d0%b4%d0%bb%d1%8f-%d0%ba%d0%b0%d1%80%d1%82%d0%b8%d0%bd/
ratings_users:
  - 4
ratings_score:
  - 12
ratings_average:
  - 3
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - css
  - shadow
---
Столкнулся с интересным примером или задачей &#8211; не знаю, как сказать. Состоит в том, чтобы сделать для картинки тень, причем внутреннюю тень. Казалось бы, задачу просто решить &#8211; с помощью box-shadow или text-shadow. Но не все так просто. В Интернете есть хорошие статьи на эту тему, в частности, на Хабре имеет очень детальный обзор данного способа.

Но пример так мне понравился, что решил его описать у себя &#8211; повторение мать учения, как говорится.

Данную задачу можно решить двумя способами. Ни один из них не является достаточно универсальным, это всего лишь выход из положения. Итак, имеется изображение, для которого нужно создать внутреннюю тень. Первый способ &#8211; это &#8220;обернуть&#8221; ее в дополнительный блок, которому прописать внутреннюю тень. Главное тут &#8211; не забыть &#8220;опустить&#8221; изображение внутри блока, чтобы тень &#8220;легла&#8221; на нее.

Код такого способа представлен ниже:

HTML:

<pre><div class="block1">
  <img src="images/charlize_theron_1.jpg" width="480" height="300" />
  
</div>
</pre>

CSS:

<pre>.block1{
  box-shadow: inset 0 0 6px 4px rgba(0,0,0,.7);
  width: 480px;
  height: 300px;
}
  .block1 img{
    position: relative;
    z-index: -2;
  }
</pre>

И результат работы этого кода:<figure id="attachment_170" style="width: 566px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/block-outer.png" alt="Картинка, обернутая в блок" width="566" height="463" class="size-full wp-image-170" />][1]<figcaption class="wp-caption-text">Картинка, обернутая в блок</figcaption></figure> 

Все хорошо &#8211; просто и работает. Единственный минус &#8211; нарушение семантики HTML-кода. Ведь, чтобы добавить для картинки всего лишь тень, потребовалось создать лишний HTML-элемент, тем самым засоряя документ.

Второй способ &#8211; более правильный с точки зрения семантики. Чтобы &#8220;набросить&#8221; тень на изображение, нужно поместить его в блок в качестве фонового изображения. В остальном все остается точно таким же, как и в первом примере. Также создается внутренняя тень для блока, но при этом нет необходимости &#8220;опускать&#8221; картинку с помощью z-index.

Код второго способа показан ниже:

HTML очень прост:

<pre>
  

<div class="block2">
  
</div>

</pre>

CSS:

<pre>.block2{
  box-shadow: inset 0 0 12px 8px rgba(0,0,0,.6);
  width: 481px;
  height: 361px;
  background: url(images/charlize_theron_2.jpg) 0 0 no-repeat;
}
</pre>

Картинка &#8211; результат работы этого кода:<figure id="attachment_171" style="width: 561px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/block-inside.png" alt="Картинка, вложенная в блок в качестве фонового изображения" width="561" height="501" class="size-full wp-image-171" />][2]<figcaption class="wp-caption-text">Картинка, вложенная в блок в качестве фонового изображения</figcaption></figure> 

Код более краткий. Единственный минус &#8211; изображение должно быть только в качестве фона для блока.

На этом все.

Оцените статью:  
<span id="post-ratings-169" class="post-ratings" data-nonce="830520a7af"><img id="rating_169_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(169, 1, '1 Star');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_169_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(169, 2, '2 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_169_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(169, 3, '3 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_169_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(169, 4, '4 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_169_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(169, 5, '5 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>3,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_169_text"></span></span><span id="post-ratings-169-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/block-outer.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/block-inside.png