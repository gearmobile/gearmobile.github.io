---
title: 'Photoshop &#8211; трансформация прямоугольного выделения'
author: gearmobile
layout: post
permalink: /photoshop-%d1%82%d1%80%d0%b0%d0%bd%d1%81%d1%84%d0%be%d1%80%d0%bc%d0%b0%d1%86%d0%b8%d1%8f-%d0%bf%d1%80%d1%8f%d0%bc%d0%be%d1%83%d0%b3%d0%be%d0%bb%d1%8c%d0%bd%d0%be%d0%b3%d0%be-%d0%b2%d1%8b%d0%b4%d0%b5/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Photoshop для кодера
tags:
  - photoshop
---
В одной из предыдущих статей я описывал способ определения радиуса скругления элемента на макете Photoshop &#8211; &#8220;[Радиус скругления углов на psd-макете][1]&#8220;. По прошествии некоторого времени мне стало очевидно, что вышеназванный обзор оказался неполным и с одной неточностью. В чем же заключаются эти два недочета? В этой статье я попытаюсь исправить ситуацию. Тем более, что ответ на один из вопросов меня интересовал, скажем так, существенно. А вторая неточность может серьезно сказаться на качестве верстки. Точнее &#8211; на соответствие сверстанного HTML-шаблона своему оригиналу &#8211; psd-макету.

Оба недочета практически взаимосвязаны между собой, поэтому логично было объединить их описание в один материал. Итак, приступаю к разбору.

Первый вопрос. Трансформация прямоугольного выделения (Rectangular Marquee). Допустим, необходимо выделить какой-либо участок или элемент на psd-макете. Как обычно, выбираю инструмент выделения на панели Photoshop. И произвожу само выделение. Но бывает так, что после того, как выделение уже построено, его нужно изменить. Увеличить высоту или ширину. Или же наоборот &#8211; уменьшить. Каким образом нужно поступить в случае?

Все просто. Для изменения размеров выделения его нужно перевести в режим трансформирования. Проще всего это выполнить с помощью сочетания горячих клавиш Ctrl+T. Легко запомнить, Т &#8211; трансформирование. Как только выделение переводится в режим изменения, внешний вид его меняется. Появляются квадратные маркеры на всех четырех углах, и посередине вcех четырех сторон. Мышкой захватываю нужный мне маркер и тяну в необходимую сторону.

Чтобы легче было представить, как это выглядит на деле, достаточно взглянуть на рисунок &#8220;Трансформация выделения&#8221; ниже.

С первым вопросом разобрались. Приступаю ко второму. В чем же заключается неточность, которая может &#8220;сгубить&#8221; шаблон? В неверно измеренном радиусе скругления. В предыдущей статье строился квадрат выделения для измерения радиуса скругления. Причем, углы квадрата должны были совпасть с точкой скругления элемента. Так вот, весь вопрос заключается в том, что точкой скругления должна считаться та, где заканчивается сплошной цвет и начинается цветовой переход.

Если максимально увеличить участок элемента, где нарисовано скругление, то попиксельно можно увидеть этот цветовой переход. Вся тонкость заключается в том, чтобы поймать эту точку. В зависимости от цвета заливки, это может быть достаточно трудной задачей. Тут нужна внимательность и точность.

Ниже представлен рисунок, на котором есть ответы на оба вопроса:<figure id="attachment_463" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/transform-marqee-600x467.png" alt="Трансформация выделения Photoshop" width="600" height="467" class="size-medium wp-image-463" />][2]<figcaption class="wp-caption-text">Трансформация выделения Photoshop</figcaption></figure> 

На этом можно закончить этот краткий обзор.

Оцените статью:  
<span id="post-ratings-461" class="post-ratings" data-nonce="5cc4931f5c"><img id="rating_461_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(461, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_461_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(461, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_461_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(461, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_461_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(461, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_461_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(461, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_461_text"></span></span><span id="post-ratings-461-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=106 "Радиус скругления углов на psd-макете"
 [2]: http://localhost:7788/third/wp-content/uploads/2013/07/transform-marqee.png