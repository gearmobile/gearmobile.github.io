---
title: 'CSS &#8211; почему треугольник это треугольник'
author: gearmobile
layout: post
permalink: /css-%d0%bf%d0%be%d1%87%d0%b5%d0%bc%d1%83-%d1%82%d1%80%d0%b5%d1%83%d0%b3%d0%be%d0%bb%d1%8c%d0%bd%d0%b8%d0%ba-%d1%8d%d1%82%d0%be-%d1%82%d1%80%d0%b5%d1%83%d0%b3%d0%be%d0%bb%d1%8c%d0%bd%d0%b8%d0%ba/
ratings_users:
  - 6
ratings_score:
  - 20
ratings_average:
  - 3.33
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - css
---
Смешное и нелепое название для статьи, но лучшего придумать не мог, так как это, по моему мнению, наиболее точно отвечает своей задаче. А точнее &#8211; задает вопрос &#8211; почему при создании треугольников на CSS с помощью псевдоэлементов :before и :after получаются именно треугольники? Методика создания таких треугольников хорошо расписана в Интернете, повторять не буду. Кому интересно, легко ее найдет. Вопрос как раз в том, почему в итоге получаются треугольники, а не прямоугольники, к примеру?

Начнем сначала и посмотрим, а как вообще браузер рисует границы для блоков. Если вы думаете (и я раньше), что браузеры генерируют границы в виде прямоугольных блоков, то глубоко ошибаетесь. Ниже покажу, как я сам раньше представлял себе этот вопрос, и как он выглядит на самом деле.

Как раньше представлял:<figure id="attachment_154" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-prev-600x480.jpg" alt="Ошибочное представление границ блока" width="600" height="480" class="size-medium wp-image-154" />][1]<figcaption class="wp-caption-text">Ошибочное представление границ блока</figcaption></figure> 

Как есть на самом деле:<figure id="attachment_155" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-now-600x520.jpg" alt="Правильное представление границ блока" width="600" height="520" class="size-medium wp-image-155" />][2]<figcaption class="wp-caption-text">Правильное представление границ блока</figcaption></figure> 

То есть, браузер отрисовывает границы под углом в 45 градусов. Точно также, как делают оконные рамы, если &#8220;на пальцах&#8221;.

Ну хорошо, с этим разобрались. Пусть будет так, но причем здесь угол в границах и треугольник? Для этого продолжим наше небольшое исследование. Оставим подопытный прямоугольник и начнем его понемногу &#8220;урезать&#8221;.

Сначала уберем у него высоту и ширину. В результате получиться такая картина:<figure id="attachment_156" style="width: 530px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-without-height-and-width.jpg" alt="Блок без ширины и высоты" width="530" height="451" class="size-full wp-image-156" />][3]<figcaption class="wp-caption-text">Блок без ширины и высоты</figcaption></figure> 

Теперь уберем нижнюю границу у этого блока и получим такое:<figure id="attachment_157" style="width: 530px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-without-border-bottom.jpg" alt="Блок без нижней границы" width="530" height="451" class="size-full wp-image-157" />][4]<figcaption class="wp-caption-text">Блок без нижней границы</figcaption></figure> 

Ну а теперь осталось дело за малым &#8211; сделаем левую и правую границы без цвета, на языке CSS &#8211; transparent.

Вуаля:<figure id="attachment_158" style="width: 530px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle.jpg" alt="Блок с прозрачными боковыми границами" width="530" height="451" class="size-full wp-image-158" />][5]<figcaption class="wp-caption-text">Блок с прозрачными боковыми границами</figcaption></figure> 

Вот и получился треугольник на CSS. Оказалось &#8211; все просто и логично.

Сделаем небольшой анализ получившегося. В результате мы имеем блок, у которого нижней границы нет, а боковые границы имеют прозрачность. Визуально в окне браузера отрисовывается треугольник, хотя на самом деле &#8211; это блок. Как он был блоком, так и остался. Все остальное &#8211; визуальный обман, который прекрасно работает.

Точно также можно создавать треугольник, который &#8220;смотрит&#8221; влево, вправо, вверх. Просто нужно поменять прозрачные границы для этого блока.

Например, для треугольника, который смотрит вправо, нужно сделать верхнюю и нижнюю границы прозрачными, левую оставить &#8220;как есть&#8221;, а правую границу убрать.

Оцените статью:  
<span id="post-ratings-153" class="post-ratings" data-nonce="f79f76a08d"><img id="rating_153_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(153, 1, '1 Star');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_153_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(153, 2, '2 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_153_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(153, 3, '3 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_153_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(153, 4, '4 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_153_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(153, 5, '5 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>6</strong> votes, average: <strong>3,33</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_153_text"></span></span><span id="post-ratings-153-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-prev.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-now.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-without-height-and-width.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle-without-border-bottom.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2013/11/css-triangle.jpg