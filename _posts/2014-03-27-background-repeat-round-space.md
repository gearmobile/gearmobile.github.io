---
title: Background-repeat и его значения round и space
author: gearmobile
layout: post
permalink: /background-repeat-round-space/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Статьи по CSS
tags:
  - background-repeat
  - round
  - space
---
Помимо хорошо известных четырех значений свойства background-repeat &#8211; repeat, no-repeat, repeat-x, repeat-y, в спецификации CSS3 появились еще два, с которыми я познакомился совсем недавно.

Перечислим их:

  * background-repeat: **round**;
  * background-repeat: **space**;

Отлично, скажете вы! Ну и что, что же это за свойства? Мало прежних четырех? Давайте разберемся сначала, что это за свойства, а уже потом будем говорить, нужны они или не нужны.

### Свойство background-repeat: repeat

Для начала посмотрим, как работает простое и привычное нам значение **repeat**:

<pre>.rnd{
    width: 700px;
    height: 500px;
    margin: 10px;
    border: 1px solid #000;
    background-image: url(img/ChristinaVujnich.jpg);
    background-position: top left;
    background-repeat: repeat;
  }
  </pre><figure id="attachment_1075" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/background-repeat_repeat-600x457.jpg" alt="Свойство background-repeat: repeat" width="600" height="457" class="size-medium wp-image-1075" />][1]<figcaption class="wp-caption-text">Свойство background-repeat: repeat</figcaption></figure> 

Видим, как браузер аккуратно сделал все, что мы от него требовали &#8211; размножил фоновое изображение по горизонтали и по вертикали. Что не вместилось в блок, то было обрезано. Получилось несколько некрасиво; но зато &#8211; что требовали.

### Свойство background-repeat: round

В спецификации CSS3 появилось одно из двух значений свойства background-repeat, которое делает попытку исправить ситуацию и выполнять &#8220;заливку&#8221; фона более красиво и &#8220;интеллектуально&#8221;. Это значение называется **round** &#8211; от английского округлять.

Работает оно по следующему принципу &#8211; изображение размножается по вертикали и горизонтали фона блока, как и прежде. Но при этом браузер определяет, сколько раз удалось поместить изображение в блок без обрезки (по вертикали и по горизонтали). Сколько &#8220;целых&#8221; раз удалось поместить &#8211; столько раз он и помещает. А с оставшимся пустым пространством он поступает так &#8211; растягивает изображение по вертикали и горизонтали, чтобы равномерно заполнить это пустое пространство.

Пример показан ниже:

<pre>.rnd{
    width: 700px;
    height: 500px;
    margin: 10px;
    border: 1px solid #000;
    background-image: url(img/ChristinaVujnich.jpg);
    background-position: top left;
    background-repeat: round;
  }
  </pre><figure id="attachment_1076" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/background-repeat_round-600x457.jpg" alt="Свойство background-repeat: round" width="600" height="457" class="size-medium wp-image-1076" />][2]<figcaption class="wp-caption-text">Свойство background-repeat: round</figcaption></figure> 

Результат получился не слишком красивый, конечно. Но зачет &#8211; попытка сделана )). А если быть более точным и без всякого &#8220;юмора&#8221;, то такой способ хорошо подойдет для фоновых изображений небольшого размера.

### Свойство background-repeat: space

Еще одно значение свойства background-repeat из спецификации CSS3, призванное решить проблему красивого размещения фонового изображения в блоке элемента, это значение **space**.

Принцип работы этого свойства аналогичен значению **round** &#8211; браузер также считает количество целых &#8220;вхождений&#8221; изображения в фон элемента. Но вот с пустым пространством он поступает несколько иначе. Браузер равномерно распределяет его между изображениями (размер которых он оставляет неизменными).

Чтобы было понятно, о чем идет речь, посмотрите на пример ниже:

<pre>.rnd{
    width: 700px;
    height: 500px;
    margin: 10px;
    border: 1px solid #000;
    background-image: url(img/ChristinaVujnich.jpg);
    background-position: top left;
    background-repeat: space;
  }
  </pre><figure id="attachment_1077" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/background-repeat_space-600x474.jpg" alt="Свойство background-repeat: space" width="600" height="474" class="size-medium wp-image-1077" />][3]<figcaption class="wp-caption-text">Свойство background-repeat: space</figcaption></figure> 

Мною намеренно были изменены размер блока, для которого &#8220;прописывалось&#8221; фоновое изображение; и размер самого изображения также. Все было сделано с целью более наглядного представления, как работает значение **space** для свойства background-repeat.

На рисунке выше хорошо видно, как браузер равномерно распределил пустое пространство по вертикали и горизонтали между изображениями.

### Значения Round & Space &#8211; поддержка браузерами

В заключение осталось упомянуть последнее &#8211; какими браузерами поддерживаются оба значения свойства background-repeat. Похвастаться особо нечем &#8211; только два браузера на момент написания этой статьи поддерживают **space** и **round**. Первый &#8211; это **Google Chrome** начиная с **v.32**. А вот второй браузер, который может похвастаться (держитесь крепче за стул!) &#8211; это **Internet Explorer v10**.

### Поддержка с помощью Modernizr

В библиотеку Modernizr включена (благодаря ходатайству Louis Lazaris) поддержка значений **round** и **space** CSS-свойства background-repeat с помощью соответствующих классов `bgrepeatspace` и `bgrepeatround`. Поэтому, теперь можно использовать эту библиотеку для определения возможности поддержки в браузерах.

Например, таким кодом:

<pre>.element {
    width: 550px;
    height: 400px;
    background: transparent url(bg.jpg) repeat 0 0; /* for all browsers */
  }

  .bgrepeatspace .element {
    background-repeat: space; /* for supporting browsers */
  }
  </pre>

### Заключение

Вот, в принципе, и все по значениям **round** и **space** свойства background-repeat. В статье активно использовались мысли (и даже код, когда шла речь о Modernizr) из источника:

[CSS3′s ‘space’ and ‘round’ Values for background-repeat][4]

Оцените статью:  
<span id="post-ratings-1073" class="post-ratings" data-nonce="19d97d829f"><img id="rating_1073_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1073, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1073_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1073, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1073_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1073, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1073_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1073, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1073_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1073, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_1073_text"></span></span><span id="post-ratings-1073-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/03/background-repeat_repeat.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2014/03/background-repeat_round.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2014/03/background-repeat_space.jpg
 [4]: http://www.impressivewebs.com/space-round-css3-background/ "CSS3′s ‘space’ and ‘round’ Values for background-repeat"